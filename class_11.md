## PANDAS

### JUPYTER NOTEBOOK
`Shift + Enter` - run current cell

### PANDAS
This is how the data is stored in Pandas (keys - colums, values - rows)

    people = {
        "first": ["John", "Jane", "Jim"],
        "last": ["Doe", "Doe", "Jackson"],
        "email": ["johndoe@email.com", "janedoe@email.com", "jimjackson@email.com"]
    }

`import pandas as pd` - convention;  
`df = pd.read_csv('path/to/your/file.csv')` - import file as dataframe (you can see the dataframe by runing df - 20 columns by default);  
`df.shape` - will show number of rows and columns;  
`df.info()` - rows, columns and data type;  
`pd.set_option('display.max_columns', 85)` - set number of columns to display;  
`pd.set_option('display.max_rows', 85)` - set number of columns to display;  
`df.head(10)`, `df.tail(15)` - display number of first/last rows (default value - 5);  
`pd.DataFrame(dict)` - creare DF from a dictionary;  

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

#### Methods
`.value_counts()` - returns count;  






[Go back](./README.md)
