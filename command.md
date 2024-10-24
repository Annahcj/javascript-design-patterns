# Command Design Pattern

The command design pattern is a behavioural design pattern that turns a request or operation into an object.   
Rather than calling the receiver (receiver of requests) directly, we encapsulate this in a class to promote separation of concerns and re-usability, as multiple interfaces may invoke the same requests.   

e.g. A full stack application with event handling in the UI. Multiple event handlers call the same api requests, so we use the command pattern to abstract this out into separate command classes.   

Another element to the command pattern is undo/transactional functionality.   
Add an undo method to each command class, and the invoker will keep track of a stack of invoked commands.   
To undo a command, pop it off the stack and call the command's undo method.   

There are three main components:
1. Command Interface: The interface for the command object.
2. Concrete Commands: There can be multiple commands all implementing the command interface.
3. Receiver: The object receiving the requests - this could be an api or some complex business logic in another layer.
4. Invoker: The object executing the commands - this could be a UI interface

**Command pattern with support for undo operations**
```
interface Command {
  execute: () => void;
  undo: () => void;
}

class FileManager {
  private files: Record<string, string> = {};

  create(fileName, fileContents) {
    console.log('Creating the file', { fileName, fileContents });
    this.files[fileName] = fileContents; // ignore duplicate file names for this example
  }
  rename(oldFileName, newFileName) {
    console.log(`Renaming the file ${oldFileName} to ${newFileName}`);
    const fileContents = this.files[oldFileName];
    delete this.files[oldFileName];
    this.files[newFileName] = fileContents;
  }
  delete(fileName) {
    console.log(`Deleting the file ${fileName}`);
    delete this.files[fileName];
  }
  getContents(fileName) {
    return this.files[fileName];
  }
}

class CreateFileCommand implements Command {
  private receiver: FileManager;
  private fileName: string;
  private fileContents: string;

  constructor(receiver, fileName, fileContents) {
    this.receiver = receiver;
    this.fileName = fileName;
    this.fileContents = fileContents;
  }

  execute() {
    this.receiver.create(this.fileName, this.fileContents);
    console.log('Calling the receiver to create the file');
  }
  undo() {
    this.receiver.delete(this.fileName);
    console.log('Calling the receiver to undo the file creation');
  }
}

class DeleteFileCommand implements Command {
  private receiver: FileManager;
  private fileName: string;
  private fileContents: string;

  constructor(receiver, fileName) {
    this.receiver = receiver;
    this.fileName = fileName;
    this.fileContents = receiver.getContents(fileName);
  }

  execute() {
    this.receiver.delete(this.fileName);
    console.log('Calling the receiver to delete the file');
  }
  undo() {
    this.receiver.create(this.fileName, this.fileContents);
    console.log('Calling the receiver to undo the file deletion');
  }
}

class RenameFileCommand implements Command {
  private receiver: FileManager;
  private oldFileName: string;
  private newFileName: string;

  constructor(receiver, oldFileName, newFileName) {
    this.receiver = receiver;
    this.oldFileName = oldFileName;
    this.newFileName = newFileName;
  }

  execute() {
    this.receiver.rename(this.oldFileName, this.newFileName);
    console.log('Calling the receiver to rename the file');
  }
  undo() {
    this.receiver.rename(this.newFileName, this.oldFileName);
    console.log('Calling the receiver to undo the file rename');
  }
}

class Invoker {
  private commands: Command[] = [];

  executeCommand(command: Command) {
    command.execute();
    this.commands.push(command);
  }
  undo() {
    if (this.commands.length === 0) {
      console.log('There are no actions to undo');
      return;
    }
    const lastCommand = this.commands.pop() as Command;
    console.log('Undoing the last action', { command: lastCommand });
    lastCommand.undo();
  }
}

// Client code
const fileManager = new FileManager();
const invoker = new Invoker();
invoker.executeCommand(
  new CreateFileCommand(
    fileManager,
    'file.txt',
    'This is the content of the new file'
  )
);
invoker.executeCommand(
  new RenameFileCommand(fileManager, 'file.txt', 'new-file.txt')
);
invoker.undo(); // changes file name back to file.txt
invoker.executeCommand(new DeleteFileCommand(fileManager, 'file.txt'));
```