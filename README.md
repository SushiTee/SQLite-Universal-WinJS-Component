# SQLite Universal WinJS Component
SQLite Universal WinJS Component for Javascript Windows Store Apps running on the Windows 10 Universal App Platform.

## Setup

_SQLite Universal WinJS_ consists of two parts: 1) WinRT C++ universal component named
_SQLite3Component_ and 2) A JavaScript file called _SQLite.js_ that builds
upon the component and simplifies use.

To use this component, copy the _SQLiteUniversalWinJS_ folder to the root of your app's solution folder.
Then in Visual Studio, go to File -> Add -> Existing Project, and choose the file _SQLiteUniversalWinJS.vcxproj_ found in
*[YourSolutionFolder]\SQLiteUniversalWinJS\*
<br>
Next, add a reference to the component in your app solution's main project in Visual Studio by going to Project -> Add Reference ... ,
where you go to Projects, and enable the _SQLiteUniversalWinJS_ project as a reference.
<br>
Finally, copy the JavaScript file _SQLite.js_ from the _WinRT Javascript Helper Files_ folder to the _js_ folder in your solution's
main project, and reference it in your _default.html_ file to use it.

## Usage

The _SQLite3JS_ namespace provides an async JavaScript API for SQLite. It is built
around the `Database` object that can be obtained using `SQLite3JS.openAsync()`.
The API was inspired by [node-sqlite3][2].

## Examples

```javascript
var dbPath = Windows.Storage.ApplicationData.current.localFolder.path + '\\db.sqlite';
SQLite3JS.openAsync(dbPath)
.then(function (db) {
  return db.runAsync('CREATE TABLE Item (name TEXT, price REAL, id INT PRIMARY KEY)')
  .then(function () {
    return db.runAsync('INSERT INTO Item (name, price, id) VALUES (?, ?, ?)', ['Mango', 4.6, 123]);
  })
  .then(function () {
    return db.eachAsync('SELECT * FROM Item', function (row) {
      console.log('Get a ' + row.name + ' for $' + row.price);
    });
  })
  .then(function () {
    db.close();
  });
});
```
## Credits
This is a port of the Windows 8.1 Component by Dave Risney found at https://code.msdn.microsoft.com/windowsapps/Universal-JavaScript-5728abdb
<br>
The project was changed to be independent of the *SQLite for Universal App Platform* extension and with the possibility to use database encryption.
<br>
For the encryption *wxSQLite* is used: http://wxcode.sourceforge.net/components/wxsqlite3/
<br>
For the database function the project *SQLite3-WinRT* is used as it fits my needs better: https://github.com/doo/SQLite3-WinRT		    
