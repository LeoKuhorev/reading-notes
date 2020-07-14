## PANDAS

### JUPYTER NOTEBOOK
`Shift + Enter` - run current cell

### PANDAS

#### Import
`import pandas as pd` - convention;  

This is how the data is stored in Pandas (keys - colums, values - rows)

    people = {
        "first": ["John", "Jane", "Jim"],
        "last": ["Doe", "Doe", "Jackson"],
        "email": ["johndoe@email.com", "janedoe@email.com", "jimjackson@email.com"]
    }

![DataFrame Representation](./assets/dataframe.svg)

`pd.Series([1, 3, 5, 8])` - create `series` object;  
`pd.date_range('20130101', periods=6)` - create DF with dates;  
`df = pd.read_csv('path/to/your/file.csv')` - import file as dataframe (you can see the dataframe by runing df - 20 columns by default);  
`df.shape` - will show number of rows and columns;   
`pd.set_option('display.max_columns', 85)` - set number of columns to display;  
`pd.set_option('display.max_rows', 85)` - set number of columns to display;   
`pd.DataFrame(dict)` - creare DF from a dictionary;  
`df.describe()` - shows a quick statistic summary of your data;  

#### Accessing data
`df['columnName']` or `df.columnName`- returns `series` object with rows in selected columns;  
`df[['column1Name', 'column2Name']]` - return `dataframe` that is filtered to the specific columns;  
`df.columns` - returns list of columns;  
`df.iloc[0]` - [index location] - returns `series` with 1st row;  
`df.iloc[[0, 1]]` - returns `dataframe` with 2 rows;  
`df.iloc[[0, 1], 2]` - returns `series` with 2 rows of the 3rd column;  
`df.iloc[[0, 1], [1, 2]]` - returns `dataframe` with 2 rows and 2 columns;  
`df.loc[0]` - [index location] - returns `series` with 1st row;  
`df.loc[[0, 1]]` - returns `dataframe` with 2 rows;  
`df.loc[[0, 1], columnName]` - returns `series` with 2 rows of the `columnName`;  
`df.loc[[0, 1], [column1Name, column2Name]]` - returns `dataframe` with 2 rows and 2 columns;  
`df.loc[0:3, 'column1Name']` - last index of the slice will be included;  

#### General Methods
`df.info()` - returns rows, columns and data type; 
`df.head(10)`, `df.tail(15)` - display number of first/last rows (default value - 5); 
`df.value_counts()` - returns count of unique values in provide series;  
`df.set_index('columnName')` - set a column to be used as index (can have 2nd parameter `inplace=True` if you need df to be modified);  
`de.reset_index(inplace=True)` - reset the index;  
`df.sort_index()` - sort df by index column (takes an optional parameter `ascending=False` for reversed order);  
`df.sort_values(by='B')` - sort by values;  
`df.T` - transpose DF;  


#### Filtering
`&` - and;  
`|` - or;  
`~` - not;  
`.isin(iterable)` - returns True if the value is present in the iterable;  
Basic Syntax:

    filt = (df['ColumnName'] == 'FilterValue')
    
    # Then either just slice the df
    df[filt]

    # Or using df.loc()
    df.loc[filt, 'columnName']

More complex filters:

    filt = df['LanguageWorkedWith'].str.contains('Python', na=False)
    df.loc[filt]

#### Updating Data in Rows and Columns

`df.columns = ['Column1Name', 'Column2Name']` - change name of all columns;  
`df.columns = [x.upper() for x in df.colums]` - bring all column names to uppercase;  
`df.columns = df.columns.str.replace(' ', '_')` - replace spaces with underscores in cilumn names;  
`df.rename(columns={'old_name': 'new_name', 'old_name_2': 'new_name_2'}, inplace=True)` - rename only specific columns;  

`df.loc[2] = ['first_value', 'second_value', 'third_value']` - select a row and set its content;  
`df.loc[2, ['column_name_1', 'column_name_2']] = ['new_value_1', 'new_value_2']` - select row and specific columns and set new values;  
`df.loc[2, 'column_name'] = 'new_value'` - change a single value;  
`df.at[2, 'column_name'] = 'new_value'` - change a single value;  
`df['column_name'] = df['column_name'].str.lower()` - bring all valued in column to lowercase;  

##### Apply (can be applied on `series` and `df`):
`df['column_name'].apply(len)` - returns length of each value in column (instead of `len` can be any function);  
`df['column_name'].apply(lambda x: x.lower())` - bring all values to lowercase (won't modify the data in place); 
 
If run on DF will apply function to each column/row:
`df.apply(len, axis='columns')` - returns length of each column in DF;  
`df.apply(pd.Series.min)` or `df.apply(labmda x: x.min())`- returns min value for each column in DF;  

##### ApplyMap (works only on DF):
`df.applymap(len)` - will return DF with the `len` method applied to each element;  
`df.applymap(str.lower)` - bring the entire DF to lowercase;  

##### Map (works only on series):
`df['column_name'].map({'old_value': 'new_value', 'old_value': 'new_value'})` - substitutes the old values with the given ones (the values that we didn't change will be converted to NaN);  

##### Replace(works only on series):
`df['column_name'].replace({'old_value': 'new_value', 'old_value': 'new_value'})` - substitutes the old values with the given ones (the values that we didn't change will stay the same);





[Go back](./README.md)
