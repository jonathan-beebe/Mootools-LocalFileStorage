LocalFileStorage
===========

This Class extends the LocalStorage interface so it's more convenient for using the browser's local storage as a file storage mechanism.

For more information of *how* the data is stored, see the notes for the parent LocalStorage class.

How To Use
-------------

Initialize the Local File Storage object, then start reading and writing.

    #JS
    
    // Create the local file storage object
    var lfs = new LocalFileStorage();
    
    // Save a file. Contents can be a string, or javascript objects. 
    // All javascript objects will be json encoded.
    lfs.save('myFileName', {a:1,b:2});
    lfs.save('myOtherFile', 'Monkeys LOVE bananas!');
    
    // Read a file
    var contents = lfs.read('myFileName');
    
    // Get a list of files
    var fileList = lfs.getList();
    
    // Delete a file
    lfs.remove('myFileName');
    
Result
------

All data will be stored in the browser's HTML5 localStorage or as Cookies.

Everything is namespaced to prevent accidental collisions. So, in the above example, you'll end up with this in your browser's storage:
    
    key                value
    -----------------------------------------
    lfs.myFileName     {a:1,b:2}
    lfs.myOtherFile    'Monkeys LOVE bananas!'
    lfs.__files__      ["myFileName","myOtherFile"]
        
Options
--------

  * namespace : Optional. Default is 'lfs'. The namespace for filenames. This helps prevent collisions if there might be another bit of code trying to write to local storage with the same name.
  * fileArrayName : Optional. Default is '__files__'. The name of the array used to store the list of files being managed by the LocalFileStorage engine.

Options for parent LocalStorage class
=====================================

  * name : this will be used for security on FF<3.5. For cross browser functionality, this should not use anything other than the current domain.
  * path : used for cookie allowed path. Again, for cross browser you should not touch this.
  * duration : used for cookie duration.
