## Initial setup

- Install wordpress
- Delete all plugins @ Plugins
- Delete all posts (Hello world!) @ Posts
- Delete pages (Privacy Policy, Sample Page) @ Pages
- Change tagline @ Settings > General
- Change timezone @ Settings > General
- Change permalinks to "Post name" @ Settings > Permalinks
- Install "Classic Editor" Plugin (optional) @ Plugins
- Create a page title "Home" and publish @ Pages
- Set "Your homepage displays" to "A static page" @ Settings > Reading
- Select "Home" as the "Homepage" @ Settings > Reading
- Delete themes @ wp-content > themes
- Create folder with new theme name (e.g.:"my-custom-theme") @ wp-content > themes
- Create index.php (blank initially) @ wp-content > themes > my-custom-theme
- Create style.css @ wp-content > themes > my-custom-theme

### style.css
```css
/**
Theme Name: My Custom Theme
Author: Vinicius Santana
**/
```
- Activate theme @ Apperance > Themes
- Add screenshot.png (1200 X 900) @ wp-content > themes > my-custom-theme

## Add bootstrap
- download it from getboostrap.com
- copy folder css to wp-content > themes > my-custom-theme > css
- copy folder js to wp-content > themes > my-custom-theme > js
- create "images" folder @ wp-content > themes > my-custom-theme

## Create Templates
- Create functions.php @ wp-content > themes > my-custom-theme
- Create page.php @ wp-content > themes > my-custom-theme
- Create header.php @ wp-content > themes > my-custom-theme
- Create footer.php @ wp-content > themes > my-custom-theme
- Create single.php @ wp-content > themes > my-custom-theme
- Create archive.php @ wp-content > themes > my-custom-theme
- Create front-page.php @ wp-content > themes > my-custom-theme
- Create search.php @ wp-content > themes > my-custom-theme
- Create 404.php @ wp-content > themes > my-custom-theme

## Includes

- Create section-content.php wp-content > themes > my-custom-theme > includes

### front-page.php
```php
<?php get_header();?>
<div class="container">
  <h1><?php the_title();?></h1>
  <?php get_template_part('includes/section', 'content');?>
</div>
<?php get_footer();?>
```

### header.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <?php wp_head();?>
</head>
<body>
```

### footer.php
```php
<?php wp_footer();?>
</body>
</html>
```

### functions.php
```php
<?php

function load_css() {
  wp_register_style('bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), false, 'all');
  wp_enqueue_style('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_css');

function load_js() {
  wp_enqueue_script('jquery');
  wp_register_script('bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', 'jquery', false, true);
  wp_enqueue_script('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_js');
```

### page.php
```php
<?php get_header();?>
<div class="container">
  <h1><?php the_title();?></h1>
  <?php get_template_part('includes/section', 'content');?>
</div>
<?php get_footer();?>
```


### includes/section-content.php
```php
<?php if(have_posts()): while(have_posts()):the_post();?>
  <?php the_content();?>
<?php endwhile; else; endif;?>
```

## Custom Templates

- create `template-contactus.php` @ wp-content > themes > my-custom-theme

### template-contactus.php
```php
<?php
/*
Template Name: Contact Us
*/
?>

<?php get_header();?>
<div class="container">
  <h1><?php the_title();?></h1>
  <div class="row">
    <div class="col-lg-6">
      This is where the contact form goes
    </div>
    <div class="col-lg-6">
      <?php get_template_part('includes/section', 'content');?>
    </div>
  </div>  
</div>
<?php get_footer();?>
```

- Select the newly created `Contact US` Template @ Pages > Edit Page  Page Attributes > Template


## Custom Headers

- Create `header-secondary.php` @ wp-content > themes > my-custom-theme 

### header-secondary.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <?php wp_head();?>
</head>
<body>
This is the secondary header
```

#### E.g.: front-page.php
```php
<?php get_header('secondary');?>
<div class="container">
  <h1><?php the_title();?></h1>
  <?php get_template_part('includes/section', 'content');?>
</div>
<?php get_footer();?>
```

## Custom Footers

- Create `footer-secondary.php` @ wp-content > themes > my-custom-theme 

### footer-secondary.php
```php
This is the secondary footer
<?php wp_footer();?>
</body>
</html>
```

#### E.g.: front-page.php
```php
<?php get_header();?>
<div class="container">
  <h1><?php the_title();?></h1>
  <?php get_template_part('includes/section', 'content');?>
</div>
<?php get_footer('secondary');?>
```