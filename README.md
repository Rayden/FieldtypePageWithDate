FieldtypePageWithDate & InputfieldPageWithDate
==============================================

Module for ProcessWire - Page Reference with Date Field - Field that stores one or more references to ProcessWire pages

Modified version of the FieldtypePage module in ProcessWire with extra datetime field containing the date a page was added to the inputfield.

### To install

Copy to /site/modules/ and go to Admin > Modules > Check for new modules. 

### Requirement
Requires: InputfieldPageWithDate (will be installed automaticly)

Tested on ProcessWire 2.5.6 dev

### Setup in back-end

- install both modules:
  - **FieldtypePageWithDate**
  - **InputfieldPageWithDate**
- create a new field in ProcessWire and give it a name
  - eg. *myfriends*
- as type choose **PageWithDate**
- choose the right dereference for your needs *(all 3 modes work fine with this field)*
  - Multiple pages (PageArray) *(in this example we are using this)*
  - Single page (Page) or boolean false when none selected
  - Single page (Page) or empty page (NullPage) when none selected
- assign a selector to the field, in this example we will use users
  - **Template of selectable page(s)** *(select the user template)*
- choose a label field, since we are using users set it to name
  - **Label Field** *name*
- set an input field type, depending if you are using dereference of multiple or a single page
  - for this example we are using **AsmSelect**
- save the field and assign it to a template of choice
- Add some users/friends to the field by editing a page with this template

### Usage in front-end

In you template you can acces the field as you usualy do with any FieldtypePage.

In addition to this the new parameter "assigned" is available

#### Multiple pages

```php
if (count($page->myfriends)) {
    foreach($page->myfriends as $friend) {
        echo "id: ".$friend->id."<br>";
        echo "name: ".$friend->name."<br>";
        echo "assigned on: ".$friend->assigned."<br><br>";
    }
}
```

##### This will output something like:

id: 1031 <br>
name: johndoe <br>
assigned on: 2014-10-31 14:22:02 <br>
<br>
id: 1032 <br>
name: janedoe <br>
assigned on: 2013-04-15 23:16:38 <br>
<br>
*Note: To use your own data/time formatting set $friend->of(false); to get a unix timestamp from the database*

#### Single page

```php
echo "id: ".$page->myfriends->id."<br>";
echo "name: ".$page->myfriends->name."<br>";
echo "assigned on: ".$page->myfriends->assigned."<br>";
```

##### This will output something like:

id: 1031 <br>
name: johndoe <br>
assigned on: 2014-10-31 14:22:02 <br>
<br>
*Note: To use your own data/time formatting set $page->myfriends->of(false); to get a unix timestamp from the database*

#### Set assigned datetime manually

You can set datetime manually by assigning it to the page you add

```php
$friend = $users->get('johndoe');
$friend->assigned = "2012-01-01 12:12:12";
$page->myfriends->add($friend);
$page->of(false);
$page->save();
```
