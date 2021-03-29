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

## Custom styles

- Create  `main.css` @ wp-content > themes > my-custom-theme > css

### functions.php
```php
<?php

function load_css() {
  wp_register_style('bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), false, 'all');
  wp_enqueue_style('bootstrap');

  wp_register_style('main', get_template_directory_uri() . '/css/main.css', array(), false, 'all');
  wp_enqueue_style('main');
}

add_action('wp_enqueue_scripts', 'load_css');

function load_js() {
  wp_enqueue_script('jquery');
  wp_register_script('bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', 'jquery', false, true);
  wp_enqueue_script('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_js');
```

## Enhancing Styles

- Add a header section to the header
- Wrap the home page cotent

### main.css
```css
  header {
    background: #111;
    width: 100%;
    height: 100px;
  }

  .page-wrap {
    padding: 2rem 0;
  }
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

<header>
<header/>
```

- Add .page-wrapper to front-page, page and template-contactus
### front-page.php
```php
<?php get_header();?>
<section class="page-wrap">
  <div class="container">
    <h1><?php the_title();?></h1>
    <?php get_template_part('includes/section', 'content');?>
  </div>
</section>
<?php get_footer();?>
```
### page.php
```php
<?php get_header();?>
<section class="page-wrapper">
  <div class="container">
    <h1><?php the_title();?></h1>
    <?php get_template_part('includes/section', 'content');?>
  </div>
</section>
<?php get_footer();?>
```

### template-contactus.php
```php
<?php
/*
Template Name: Contact Us
*/
?>

<?php get_header();?>
<section class="page-wrapper">
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
</section>
<?php get_footer();?>
```

## Remove admin bar
- Uncheck Toolbar: Show Toolbar when viewing site @ Users / Your Profile

## Navigation Menu

- add menu support in functions.php
### functions.php
```php
<?php

// Load stylesheets
function load_css() {
  wp_register_style('bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), false, 'all');
  wp_enqueue_style('bootstrap');

  wp_register_style('main', get_template_directory_uri() . '/css/main.css', array(), false, 'all');
  wp_enqueue_style('main');
}

add_action('wp_enqueue_scripts', 'load_css');

// Load javascript
function load_js() {
  wp_enqueue_script('jquery');
  wp_register_script('bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', 'jquery', false, true);
  wp_enqueue_script('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_js');

// Theme Options
add_theme_support('menus');
```

- Create a menu (e.g.: `Top bar`) @ Appearance > Menus
- Add pages to menu
- Create a menu @ functions.php

### functions.php
```php
<?php

// Load stylesheets
function load_css() {
  wp_register_style('bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), false, 'all');
  wp_enqueue_style('bootstrap');

  wp_register_style('main', get_template_directory_uri() . '/css/main.css', array(), false, 'all');
  wp_enqueue_style('main');
}

add_action('wp_enqueue_scripts', 'load_css');

// Load javascript
function load_js() {
  wp_enqueue_script('jquery');
  wp_register_script('bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', 'jquery', false, true);
  wp_enqueue_script('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_js');

// Theme Options
add_theme_support('menus');

// Menus
register_nav_menus(
  array(
    'top-menu' => 'Top Menu Location',
    'mobile-menu' => 'Mobile Menu Location',
  )
);
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

<header>
  <div class="container">
    <?php 
      wp_nav_menu(
        array(
          // 'menu' => 'Top Bar',
          'theme_location' => 'top-menu',
          'menu_class' => 'top-bar'
        )
      );
    ?>
  </div>
<header/>
```

### main.css
```css
  header {
    background: #111;
    width: 100%;
    height: 100px;
  }

  .page-wrap {
    padding: 2rem 0;
  }

  header .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
  }

  header .top-bar {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
  }

  header .top-bar li a {
    padding: 0.25rem 1rem;
    color: #fff;
  }

  header .top-bar li:first-child a {
    padding-left: 0;
  }

  header .top-bar li:last-child a {
    padding-right: 0;
  }
```

### footer.php
```php

<header>
  <div class="container">
    <?php 
      wp_nav_menu(
        array(
          'theme_location' => 'footer-menu',
          'menu_class' => 'footer-bar'
        )
      );
    ?>
  </div>
<header/>

<?php wp_footer();?>
</body>
</html>
```

### functions.php
```php
<?php

// Load stylesheets
function load_css() {
  wp_register_style('bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), false, 'all');
  wp_enqueue_style('bootstrap');

  wp_register_style('main', get_template_directory_uri() . '/css/main.css', array(), false, 'all');
  wp_enqueue_style('main');
}

add_action('wp_enqueue_scripts', 'load_css');

// Load javascript
function load_js() {
  wp_enqueue_script('jquery');
  wp_register_script('bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', 'jquery', false, true);
  wp_enqueue_script('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_js');

// Theme Options
add_theme_support('menus');

// Menus
register_nav_menus(
  array(
    'top-menu' => 'Top Menu Location',
    'mobile-menu' => 'Mobile Menu Location',
    'footer-menu' => 'Footer Menu Location',
  )
);
```

# Blogging functionality

- Create a few posts and add it to  "Blog" category @ Posts

- create includes/serction-archive.php

### includes/section-archive.php
```php
<div class="card mb-3">
  <div class="card-body">
    <?php if(have_posts()): while(have_posts()):the_post();?>
      <h3><?php the_title();?></h3>
      <?php the_excerpt();?>
      <a href="<?php the_permalink();?>" class="btn btn-success">Read more</a>
    <?php endwhile; else; endif;?>
  </div>
</div>
```

### archive.php
```php
<?php get_header();?>
<section class="page-wrapper">
  <div class="container">    
    <?php get_template_part('includes/section', 'archive');?>

    <?php previous_posts_link();?>
    <?php next_posts_link();?>


  </div>
</section>
<?php get_footer();?>
```
- Change "Blog pages shows at most" to a custom value (e.g.: 3) @ Settings > Reading


## Custom category templates

- create `category-blog.php`

### category-blog.php
```php
<?php get_header();?>
<section class="page-wrapper">
  <div class="container">    
    Custom Category 
    <?php get_template_part('includes/section', 'archive');?>

    <?php previous_posts_link();?>
    <?php next_posts_link();?>


  </div>
</section>
<?php get_footer();?>
```

## Single post
### single.php
```php
<?php get_header();?>
<section class="page-wrap">
  <div class="container">
    <h1><?php the_title();?></h1>
    <?php get_template_part('includes/section', 'blogcontent');?>
  </div>
</section>
<?php get_footer();?>
```

### includes/section-blogcontent.php
- for more date formats look at php manual dates
```php
  <?php if(have_posts()): while(have_posts()):the_post();?>
    <p><?php echo get_the_date('l jS F, Y'); ?></p>
    // <p><?php echo get_the_date('d/m/Y h:i:s'); ?></p>
    <?php the_content();?>
    
    // <?php the_author();?>
    
    // <?php 
    //   $fname = get_the_author_meta('first_name');
    //   $lname = get_the_author_meta('last_name');
    //   echo $fname . ' ' . $lname;
    // ?>

    <p>Post by <?php echo $fname> <?php echo $lname; ?></p>

    <?php 
    $tags = get_the_tags();
    foreach($tags as $tag):?>
      <a href="<?php echo get_tag_link($tag->term-id);?>" class="badge-success">
        <?php echo $tag->name;?>
      </a>
    <?php endforeach;?>


    <?php 
    $categories  = get_the_category();
    foreach($categories as $cat):?>
      <a href="<?php echo get_category_link($cat -> term_id);?>">
        <?php echo $cat->name;?>
      </a>
    <?php endforeach;?>

    <?php comments_template();?>


  <?php endwhile; else; endif;?>
```
- add category to title of archive and category-blog
- wp_link_pages links sections of the same post separated by PAGE BREAK (alt + shift + p) - <!--nextpage-->
### archive.php
```php
<?php get_header();?>
<section class="page-wrapper">
  <div class="container">    
    <h1><?php echo single_cat_title();?></h1>
    <?php get_template_part('includes/section', 'archive');?>

    <?php previous_posts_link();?>
    <?php next_posts_link();?>
  </div>
</section>
<?php get_footer();?>
```

### category-blog.php
```php
<?php get_header();?>
<section class="page-wrapper">
  <div class="container">    
    <h1><?php echo single_cat_title();?></h1> 
    <?php get_template_part('includes/section', 'archive');?>

    <?php previous_posts_link();?>
    <?php next_posts_link();?>
  </div>
</section>
<?php get_footer();?>
```

- add wp_link_pages links sections of the same post separated by PAGE BREAK (alt + shift + p) - <!--nextpage-->

### single.php
```php
<?php get_header();?>
<section class="page-wrap">
  <div class="container">
    <h1><?php the_title();?></h1>
    <?php get_template_part('includes/section', 'blogcontent');?>
    <?php wp_link_pages();?>
  </div>
</section>
<?php get_footer();?>
```

## Enable post images

### functions.php
```php
<?php

// Load stylesheets
function load_css() {
  wp_register_style('bootstrap', get_template_directory_uri() . '/css/bootstrap.min.css', array(), false, 'all');
  wp_enqueue_style('bootstrap');

  wp_register_style('main', get_template_directory_uri() . '/css/main.css', array(), false, 'all');
  wp_enqueue_style('main');
}

add_action('wp_enqueue_scripts', 'load_css');

// Load javascript
function load_js() {
  wp_enqueue_script('jquery');
  wp_register_script('bootstrap', get_template_directory_uri() . '/js/bootstrap.min.js', 'jquery', false, true);
  wp_enqueue_script('bootstrap');
}

add_action('wp_enqueue_scripts', 'load_js');

// Theme Options
add_theme_support('menus');
add_theme_support('post-thumbnails');

// Menus
register_nav_menus(
  array(
    'top-menu' => 'Top Menu Location',
    'mobile-menu' => 'Mobile Menu Location',
    'footer-menu' => 'Footer Menu Location',
  )
);

// Custom Image Sizes
add_image_size('blog-large', 800, 400, true);
add_image_size('blog-small', 300, 200, true);
```

### single.php
```php
<?php get_header();?>
<section class="page-wrap">
  <div class="container">
    <?php if(has_post_thumbnail()):?>
      <img src="<?php the_post_thumbnail_url('blog-large');?>" alt="<?php the_title();?>" class="img-fluid mb-3 img-thumbnail">
    <?php endif;?>
    <h1><?php the_title();?></h1>
    <?php get_template_part('includes/section', 'blogcontent');?>
    <?php wp_link_pages();?>
  </div>
</section>
<?php get_footer();?>
```

- Plugin - force regenerate thumbnails

### includes/section-archive.php
```php

  
<?php if(have_posts()): while(have_posts()):the_post();?>
  <div class="card mb-3">
    <div class="card-body d-flex justify-content-center align-items-center">
      <?php if(has_post_thumbnail()):?>
        <img src="<?php the_post_thumbnail_url('blog-small');?>" alt="<?php the_title();?>" class="img-fluid mb-3 img-thumbnail mr-4">
      <?php endif;?>

      <div class="blog-content">
        <h3><?php the_title();?></h3>
        <?php the_excerpt();?>
        <a href="<?php the_permalink();?>" class="btn btn-success">Read more</a>   
      </div>       
    </div>
  </div>
<?php endwhile; else; endif;?>
```

### page.php
```php
<?php get_header();?>
<section class="page-wrapper">
  <div class="container">
    <h1><?php the_title();?></h1>
    <?php if(has_post_thumbnail()):?>
      <img src="<?php the_post_thumbnail_url('blog-large');?>" alt="<?php the_title();?>" class="img-fluid mb-3 img-thumbnail">
    <?php endif;?>
    <?php get_template_part('includes/section', 'content');?>
  </div>
</section>
<?php get_footer();?>
```