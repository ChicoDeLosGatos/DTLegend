# DTLegend.js
A customizable legend in Javascript for DataTables (https://datatables.net/)

<h2>Basic Usage:</h2>

<h3>HTML:</h3>

`<body>`<br/>
`...`<br/>
`<table id="`**sample_people_table**`" class="table">`<br/>
&emsp;`<thead>`<br/>
&emsp;&emsp;`<tr>`<br/>
&emsp; &emsp; &emsp;`<th>Id</th>`<br/>
&emsp; &emsp; &emsp;`<th>Name</th>`<br/>
&emsp; &emsp; &emsp;`<th>Gender</th>`<br/>
&emsp; &emsp; &emsp;`<th>Age</th>`<br/>
&emsp;&emsp;`</tr>`<br/>
&emsp;`</thead>`<br/>
&emsp;`<tbody></tbody>`<br/>
&emsp;`<tfoot id="`**sample_people_table_footer**`"></tfoot>`<br/>
`</table>`<br/>
`...`<br/>
`<script type='text/javascript' charset='utf8' src='https://cdn.datatables.net/1.10.20/js/jquery.dataTables.min.js'></script>`<br/>
`<script type='text/javascript' src='./js/dtlegendjs.min.js'></script>`<br/>
`</body>`


<h3>JS</h3>

<h4>Step 1: Set up the DataTable</h4>

`var dataTable;`<br/>
`dataTable = $('#sample_people_table').DataTable({`<br/>
&emsp;`ajax: ajax_people_query,`<br/>
&emsp;`columns: [`<br/>
&emsp;&emsp;`{ data: 'id' },`<br/>
&emsp;&emsp;`{ data: 'name' },`<br/>
&emsp;&emsp;`{ data: 'gender' },`<br/>
&emsp;&emsp;`{ data: 'age' },`<br/>
&emsp;`],`<br/>
&emsp;`createdRow: function (row, data, index) {`<br/>
&emsp;&emsp;`if (data.age < 18) $(row).css('background-color', '#98CEE5');`<br/>
&emsp;&emsp;`var gender = (data.gender == 'F') ? '#FADE80' : '#C48356';`<br/>
&emsp;&emsp;`$(row).css('background-color', gender);`<br/>
&emsp;`}`<br/>
`});`<br/>

<h4>Step 2: Set the DTLegend</h4>

`var legend;`<br/>
`legend = new DTLegend(`<br/>
&emsp;`'sample_people_table -v', [ //set the verbose attribute (-v) will show you in console dtl messages`<br/>
&emsp;&emsp;`['Men', '#FADE80'], //this will be the label 0, called lbl0 and referenced with lb0`<br/> 
&emsp;&emsp;`['Women', '#C48356'], //lbl1 (lb1)`<br/>
&emsp;&emsp;`['Teens', '#98CEE5'] //lbl2 (lb2)`<br/>
&emsp;`] // You can reference max 8 labels`,<br/>
&emsp;`toggleFilter`,<br/>
&emsp;`function(selection){`<br/>
&emsp;&emsp;`$.fn.dataTable.ext.search.push(`<br/>
&emsp;&emsp;&emsp;`function (settings, searchData, index, rowData, counter) {`<br/>
&emsp;&emsp;&emsp;&emsp;`switch(selection){`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;`case 'lbl0':`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`if(rowData.gender == 'M') return lb0;`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;`case 'lbl1':`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`if(rowData.gender == 'F') return lb1;`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;`case 'lbl2':`<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`if(rowData.age < 18) return lb3;`<br/>
&emsp;&emsp;&emsp;&emsp;`}`<br/>
&emsp;&emsp;&emsp;&emsp;`return true;`<br/>
&emsp;&emsp;`});`<br/>
`});`<br/>

`function toggleFilter(lbl){`<br/>
&emsp;`legend.filter(lbl);`<br/>
`}`


