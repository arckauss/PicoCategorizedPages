# Pico-Categorized-Pages
A little [Pico-CMS](http://picocms.org/) plugin allowing you to automatically sort (ascending or descending), position and categorize your page from your content folder.

## General Purpose

The purpose here is to be able to generate a navigation menu simply by writing the script below.
```twig
    <nav>
  		<ul>
  		{% for category in categories %}
  			<li>
  				<a href="{{ category.pages[1].url }}">{{ category.title }}</a>
  				{% if category.pages|length > 1 %}
  				<ul>
  				{% for page in category.pages %}
  					<li class="sub"><a href="{{ page.url }}">{{ page.title }}</a></li>
  				{% endfor %}
  				</ul>
  			  {% endif %}
  			</li>
  		{% endfor %}
  		</ul>
  	</nav>
```
## How-to

First, be sure to configure it properly
```php
    $config['pages_order_by'] = 'position'; // Set the pages order by position
    $config['pages'] = 'asc';               // ascending sort by default, can be 'desc'
```

A category is simply a folder inside your content folder.
The description of the folder is declared in the index.md of that folder. It is where the position in the menu and its title will be set.
The same logic applies to each file inside that folder, except they won't have any impact on the folder declaration.

Let's consider the following content structure :

    ./content
      ./Bees
        ./index.md
        ./hive.md
        ./honey.md
      ./Ants
        ./index.md
        ./queen.md
        ./solders.md
        
Index.md for Bees :

    /*
    Title: Welcome to the bees !
    Position: 1
    Category_Position: 2
    Category_Title: Beez ?!
    */
    
Will create a category at the second position (Category_Position) with the title "Beez ?!" (Category_Title) and the page itself will be titled "Welcome to the bees" and will be te first item in the list.

The same applies for hive.md :

    /*
    Title: Hive is good
    Position: 3
    */

and honey.md

    /*
    Title: The sweet honey boogie
    Position: 2
    */
    
Will output :
```html
    <nav>
      <ul>
        ...
        <li>
          <a href="yoururl../Bees/">Beez ?!</a>
          <ul>
            <li class="sub"><a href="yoururl../Bees/">Welcome to the bees !</a></li>
            <li class="sub"><a href="yoururl../Bees/honey">The sweet honey boogie</a></li>
            <li class="sub"><a href="yoururl../Bees/hive">Hive is good</a></li>
          </ul>
        </li>
      </ul>
    </nav>
```

## Installation
Simply put pico_categorized_pages.php in your plugins folder and it will be fine as it is.
But don't forget to set your config.php right as mentioned in the How-To.

## What's next ?

- Folder ignore
- Recursive categories