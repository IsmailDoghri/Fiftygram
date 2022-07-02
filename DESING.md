Final Project Fiftygram

Let's first start by the MainActivity class. Ass you can see this project only contains one main class extending AppCompatActivity and implementing ActivityCompat.OnRequestPermissionsResultCallback. This implementation will allow the app to request permission to store a photo to the user’s device; the requestPermissions() function in onCreate will then take care of the rest (when opening the app for the first time, a message should pop up asking if the app can access the device's photos). As the application created is pretty trivial, I did not find the need to create multiple classes to implement it since we are only working on one page.

Important methods: setContentView() sets the layout implemented in activity_main.xml.
findViewById() gets the unique id of the image from a class called "R" (resource).

In the choosePhoto function: setType("image/*) allows us to open an image no matter its type as long as it's an image.

In the apply function: Glide here is a static library that contains a load() method that gets our image, a apply() method that lets us apply a transformation from the library, and into() that loads the modifications made into an image view.
All the filter applications below will, therefore, use this method to transform the image.

In the save function: destroyDrawingCache() will free the resources used by the drawing cache. This should always be used after caching the drawing to clean it. 
setDrawingCacheEnabled() will then enable the drawing cache so getDrawingCache() is able to return the bitmap of the image.
MediaStore.Images.Media.insertImage() will save the image in the specified place.

Finally, onActivityResult() is a method defined in AppCompactActivity that is going to be called by the system when the we exit from the activity we opened (once a photo is selected).  
getData() gives us a path (stored here as a Uri) to the data we selected.
openFileDescriptor(), from the class getContentResolver(), that allows us to open our image (stored in the Uri) in "read" mode.
The try/catch here is to make sure to return an error message in case we attempt to open an invalid Uri.
decodeFileDesvriptor() is a method in the BitmapFactory class that will allow us to create a Bitmap objet.


Moving on to our layout, in activity_main:
Here I tried to make sure both the "Add photo" and "Save" button are distinguishable from the filters buttons. Therefore, "math_parent" in layout_width would be perfect for adapting these buttons' width to the main Layout by making sure not touch the ends using layout_margin. I also added an additional style to "Save" button that gives it a different flashy colour as this is the last step of our usage. 

onClick is fundamentally what will link the user's action to our main class specifying what method to call for every button clicked.

Finally, a more aesthetic way to present our filters was to line them 2-by-2 vertically, allowing a more readable interface, also saving space on the screen. Here the LinearLayout takes care of orienting two consecutive buttons horizontally while the main LinearLayout will skip a line every two buttons. Note that I didn't need to specify a horizontal orientation for these layouts as it is the automatic option.
