# jQuery File Upload, Simplified.

*jquery-file-upload-simplified* is fork of the popular [jQuery-file-upload](http://github.com/blueimp/jQuery-File-Upload)
library. This fork was created to strip out most of the obfuscation, while keeping things minimal.

## Setup

A minimal setup with a progress bar, drag and drop enabled, multiple files, and a status text.

**The HTML**
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Jquery File Upload, Simplified. Example.</title>
  </head>
  <body>
    <div>
        <h1>jQuery-File-Upload, Simplified.</h1>
        <p>Choose or drag a file here to upload.</p>
        
        <div class="progress">
          <div class="bar" style="width: 0%"></div>
        </div>
        
        <span class="status"></span>

        <form action="http://localhost:5000/upload" name="images" enctype="multipart/form-data" class="direct-upload">
          <input class="file-input" name="file" type="file">
        </form>
    </div>

    <script src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>
    <script src="//cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/2.3.2/js/bootstrap.min.js"></script>
    <script src="jquery.ui.widget.js"></script>
    <script src="jquery.fileupload.js"></script>
    <script src="app.js"></script><!-- JS file below -->
  </body>
</html>
```


**The Javascript (app.js)**
```javascript
$(function() {

  $('.direct-upload').each(function() {
    /* For each file selected, process and upload */

    var form = $(this)

    $(this).fileupload({
      url: form.attr('action'), // Grabs form's action src
      type: 'POST',
      autoUpload: true,
      dataType: 'json',
      add: function (event, data) {
        data.context = $('<p/>').text('Uploading...').appendTo('.status');
        data.submit();
      },
      send: function(e, data) {
        $('.progress').fadeIn(); // Display widget progress bar
      },
      progress: function(e, data){
        var percent = Math.round((e.loaded / e.total) * 100)
        $('.bar').css('width', percent + '%') // Update progress bar percentage
      },
      fail: function(e, data) {
        console.log('fail')
        data.context.text('Upload failed.');
        $('.progress').addClass('progress-danger');
      },
      success: function(data) {
        console.log('success')
      },
      done: function (event, data) {
        // When upload is done, fade out progress bar and reset to 0
        data.context.text('Upload finished.');
        $('.progress').fadeOut(300, function() {
          $('.bar').css('width', 0)
        })
      },
    })
  })
})
```

## The Upload Controller
(work-in-progress)

## License
Released under the [MIT license](http://www.opensource.org/licenses/MIT).

## Original Repo
jquery-file-upload-simplified is a fork of [jQuery-file-upload](http://github.com/blueimp/jQuery-File-Upload). This fork is simply a stripped down,
minimal copy of the original. All jquery-file-upload issues, documentation and code can be found on
their [Github page](http://github.com/blueimp/jQuery-File-Upload).
