# Extract Embedded Datasources from Tableau workbooks

This script extracts the **embedded** datasource information (SQL and tables) from Tableau workbook files (`*.twb`) and XML files (`*.xml`) in a specified directory, and saves the results to a CSV file. Embedded datasource downloads are not supported by the `tableauserverclient` SDK (https://tableau.github.io/server-client-python/docs/). 

This script was written for extracting and storing **embedded** custom SQLs in tableau into a central database. Using the csv file generated, one can then create `dbt` models to create these custom SQLs as views etc in the database and eventually publish them as tableau datasources for workbooks to access. 
 
This script will:
1. Download the Tableau workbook files (`*.twb`, `*.twbx`) using the tableauserverclient python SDK
2. Rename twbx filenames to filename.twbx.zip  
3. `unzip_file()` will unzip the renamed .zip files and get the twb files from the unzipped temp dir and move it to the `dest_dir`.
4. `extract_datasource()` will extract the SQL from `CDATA` section of the `.twb` file and table info from the `relation connection=`. Feel free to change the regex patterns in the last cell to suit your needs.

## Requirements

- Python 3.x
- pandas library
- tableauserverclient python sdk

## Usage
Run the script from VSCode or from cli using `jupyter nbconvert --to script --execute tableau_extract_ds.ipynb`.

## Output

The script outputs a CSV file named `tableau_ds_list.csv` in the destination directory, which contains the following columns:

- `filename`: the name of the Tableau workbook file or XML file.
- `match`: the extracted SQL query or datasource table name.

## License

This script is licensed under the MIT License.