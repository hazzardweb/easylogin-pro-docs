# Comments Integration

- [Standard](#standard)
- [Embedded](#embedded)

## Standard

In the standard integration you have all of the CSS and JavaScript (like in the main script version).

    <?php require_once 'app/init.php'; ?>

    <?php echo View::make('header')->render() ?>
        
    <h3 class="page-header">Comment Page Example</h3>
    <?php
        $page = '1'; // Page identifier
        $pageTitle = 'My Page'; // Friendly name for the page
        echo ajax_comments($page, $pageTitle); 
    ?>

    <?php echo View::make('footer')->render() ?>

The `ajax_comments` function will display the HTMl for the comments. The first parameter `$page` is an identifier, so for each page you have diferrent comments. The second one `$pageTitle` should be set to a name that represents that page, so you can see easily in the admin panel on which page was the comment posted.

## Embedded

The embedded integration allows you to use the comments without having to include the main script CSS and JavaScript. You may use this when don't want the comments CSS to conflict with your own site CSS.

    <html>
    <head>
        <!-- Include jQuery -->
        <script src="assets/js/vendor/jquery-1.11.1.min.js"></script>
    </head>
    <body>
        <!-- Embeded version with iframe -->
        <div id="embed_comments" style="max-width:800px"></div>
        <script src="assets/js/embed-comments.js"></script>
        <script> embedComments('#embed_comments', '1', 'My Page'); </script>
        <!-- /end -->
    </body>
    </html>

The `embedComments` function takes 3 parameters. The first one is a selector (id/class) of the div where you want the comments to be displayed (in this case `#embed_comments`). <br>
The second one is an identifier, so for each page you have diferrent comments. <br>
The third one should be set to a name that represents that page, so you can see easily in the admin panel on which page was the comment posted.

For a complete example that includes the log in and sign up see `extra/examples/modal/comments.php` from the archive.
