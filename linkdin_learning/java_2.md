# SWING

- packages are usually mentioned using the reverse domain format

## Reading data from a files

- first get the path of the file using `FileSystems.getDefault().getPath(<root of search>,<name of the file> )` from java.nio.file.* to a Path object

- you can store the file being read in a List<string>.

- if you have a call in the methd which can throw an error, you need to suround the block with a try, catch block or specify the error it can throw in the declaration.

- you can read all lines of the file using the `Files.readAllLines(<Path object of the file>)`

## Making a basic GUI

- create a new project with new application  window option in the swing library

- select buttons you want to work togeteher to make a button group

- use a listner class to do some actions depending on input

- `AbstractTableModel` interface is used to set data source for a table. and we can attach the instance of AbstractTableModel using `Table.setModle(data)`



