# node-red-contrib-salesforce

A set of [Node-RED](http://www.nodered.org) nodes to interact with Salesforce and Force.com.

## Install
-------

Run the following command in the root directory of your Node-RED install

```
npm install node-red-contrib-salesforce
```

## Usage

### Query

<p>Executes a SOQL query.</p>
<p>The query can be configured in the node, however if left blank, the query should be set in an incoming message on <code>msg.soql</code>.</p>
<p>See the <a href="https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl" target="_blank">Salesforce SOQL documentation</a> for more information.</p>

### DML

<p>Executes an insert, update, upsert or delete DML statement.</p>
<p><b>Insert Action</b></p>
<p>This action inserts the contents of <code>msg.payload</code> and returns the newly created ID.</p>
<pre>{
firstname: "Nikola",
lastname: "Tesla"
}</pre>
<p><br/><b>Update Action</b></p>
<p>This action updates the specified record with the the contents of <code>msg.payload</code>. It assumes that the payload contains an <code>id</code> property with the id of the record to be updated.</p>
<pre>{
id: "00337000002uFbW",
firstname: "Nikola",
lastname: "Tesla"
}</pre>
<p><br/><b>Upsert Action</b></p>
<p>The upsert action matches contents of the <code>msg.payload</code> with existing records by comparing values of one field. If you don’t specify a field when calling this action, the operation uses the id value in the <code>msg.payload</code> to match with existing records to update. Alternatively, you can specify a field to use for matching in <code>msg.externalId</code>. This field must be marked as external ID. If a matching record is not found, a new records is inserted.</p>
<p>Sample <code>msg.payload</code> to be used with an external id.</p>
<pre>{
firstname: "Nikola",
lastname: "Tesla"
}</pre>
<p>Sample <code>msg.externalId</code> specifying the field and value to be used for matching.</p>
<pre>{
field: "Ext_ID__c",
value: "12345"
}</pre>
<p>If record(s) are updated, the resulting payload will resemble:</p>
<pre>{
"payload": {
"success": true,
"object": "contact",
"id": {
  "field": "Ext_ID__c",
  "value": "12345"
},
"action": "update"
}
}</pre>
<p>If a new record is inserted, the resulting payload will resemble the following containing the id of the newly created record:</p>
<pre>{
"payload": {
"success": true,
"object": "contact",
"id": "00337000002uwUVAAY",
"action": "insert"
}
}</pre>
<p><br/><b>Delete Action</b></p>
<p>This action deletes the record specified by the id property in <code>msg.payload</code>.</p>
<pre>{
"id": "00337000002uwUVAAY"
}</pre>
<p>See the <a href="https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_dml_section.htm#apex_dml_insert" target="_blank">Apex DML Operations</a> for more information.</p>
