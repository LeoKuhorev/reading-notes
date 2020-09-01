## Django Models

### Relationships

- one to one (OneToOneField)
- one to many (ForeignKey)
- many to many (ManyToManyField)

### Field attributes

- `help_text=''` - provides a text label for HTML forms (e.g. in the admin site), as described above;
- `verbose_name=''` - human-readable name for the field used in field labels. If not specified, Django will infer the default verbose name from the field name;
- `default=''` - the default value for the field. This can be a value or a callable object, in which case the object will be called every time a new record is created;
- `null=True` - if True, Django will store blank values as NULL in the database for fields where this is appropriate (a CharField will instead store an empty string). The default is False;
- `blank=True`: if True, the field is allowed to be blank in your forms. The default is False, which means that Django's form validation will force you to enter a value. This is often used with null=True , because if you're going to allow blank values, you also want the database to be able to represent them appropriately;
- `choices=[('one', 'One'), ('two', 'Two')]`: A group of choices for this field. If this is provided, the default corresponding form widget will be a select box with these choices instead of the standard text field;
- `primary_key=True`: If True, sets the current field as the primary key for the model (A primary key is a special database column designated to uniquely identify all the different table records). If no field is specified as the primary key then Django will automatically add a field for this purpose.

### Field types

`CharField` - is used to define short-to-mid sized fixed-length strings. You must specify the `max_length` of the data to be stored;  
`TextField` - is used for large arbitrary-length strings. You may specify a `max_length` for the field, but this is used only when the field is displayed in forms (it is not enforced at the database level);  
`IntegerField` - is a field for storing integer (whole number) values, and for validating entered values as integers in forms;  
`DateField` and `DateTimeField` - are used for storing/representing dates and date/time information (as Python `datetime.date` in and `datetime.datetime` objects, respectively). These fields can additionally declare the (mutually exclusive) parameters `auto_now=True` (to set the field to the current date every time the model is saved), `auto_now_add` (to only set the date when the model is first created) , and `default` (to set a default date that can be overridden by the user);  
`EmailField` - is used to store and validate email addresses;
`FileField` and `ImageField` - are used to upload files and images respectively (the ImageField simply adds additional validation that the uploaded file is an image). These have parameters to define how and where the uploaded files are stored;  
`AutoField` is a special type of IntegerField that automatically increments. A primary key of this type is automatically added to your model if you don’t explicitly specify one;  
`ForeignKey` is used to specify a one-to-many relationship to another database model (e.g. a car has one manufacturer, but a manufacturer can make many cars). The "one" side of the relationship is the model that contains the "key" (models containing a "foreign key" referring to that "key", are on the "many" side of such a relationship);  
`ManyToManyField` is used to specify a many-to-many relationship (e.g. a book can have several genres, and each genre can contain several books). In our library app we will use these very similarly to ForeignKeys, but they can be used in more complicated ways to describe the relationships between groups. These have the parameter `on_delete` to define what happens when the associated record is deleted.

[Go back](./README.md)