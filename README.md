Meteor Autoform i18n
====================

Internationalization for [aldeed:autoform](http://github.com/aldeed/meteor-autoform) powered by [tap:i18n](https://github.com/TAPevents/tap-i18n).  
This package automatically attaches reactive labels, input placeholders and select options to your forms created through Autoform.  

UPDATE: To get reactively translated default Autoform error messages, additionally use [gwendall:simple-schema-i18n](https://github.com/gwendall/meteor-simple-schema-i18n).  

Installation  
------------

``` sh
meteor add gwendall:autoform-i18n
```

How-to
------

**1. Create an i18n file with your translations**  

\*.i18n.json files contain the values that the package will apply to your schema. For each schema field, you can pass the following values:

- ``label``: Will be set as a label in your autoform
- ``placeholder``: Will be set as a text input / textarea placeholder or select first option, depending on your input type
- ``options``: Will be the options available in your selects, radioboxes or checkboxes for the given field.

If you explicitely defined a ``label``, ``placeholder`` or ``options`` in your schema, the package will not overwrite them with translations. Don't declare those fields in your SimpleSchema object for the package to take care of them for you.

**2. Define a simple-schema for your collection and call Schema.i18n(json_path)**  

``json_path`` is the path allowing the package to find your translations for this schema in your i18n files.  

Example
-------

Example
-------

**/i18n/en.i18n.json**  
``` json
{
  "schemas": {
    "posts": {
      "title": {
        "label": "Title",
        "placeholder": "Enter a title for your post"
      },
      "category": {
        "label": "Category",
        "placeholder": "Select a category",
        "options": {
          "announcements": "Announcements",
          "packages": "Packages",
          "ama": "AMA",
          "news": "News"
        }
      }
    }
  }
}
```  

**/i18n/fr.i18n.json**  
``` json
{
  "schemas": {
    "posts": {
      "title": {
        "label": "Titre",
        "placeholder": "Veuillez saisir le titre de votre publication"
      },
      "category": {
        "label": "Categorie",
        "placeholder": "Choisissez une categorie",
        "options": {
          "announcements": "Annonces",
          "packages": "Paquets",
          "ama": "AMA",
          "news": "Nouvelles"
        }
      }
    }
  }
}

```  

**/lib/collections/.js**  
``` javascript
Posts = new Mongo.Collection("posts");
Schema = new SimpleSchema({
  "title": {
    type: String
  },
  "category": {
    type: String
  }
});
Schema.i18n("schemas.posts");
Posts.attachSchema(Schema);
```

**/client/tpl.html**  
``` html
<template name="postForm">
  {{> quickForm collection="Posts" id="insertPostForm" type="insert"}}
</template>
```
