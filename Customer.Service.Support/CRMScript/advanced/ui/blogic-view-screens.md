---
title: View screens
uid: crmscript_blogic_view
SortOrder: 70
---

**View elements** displays read-only info. These elements may **not** contain children.

## Visual components

* [Header](@blogic_header): adds a sub-header (can be made into a link)

* [Link row (Anchor line)](@blogic_anchor_line): adds a horizontal line of clickable URLs (breadcrumbs)

* [BR](@blogic_br): an HTML line-break (vertical space)

* [HR](@blogic_hr): adds a horizontal line

## Info fields v2

[Info fields v2](@blogic_info_fields_2) adds a grid of information fields.

### Example config

```crmscript
profileBaseTable = contact
profileElementName = view_contact
where.0.field = contact.contact_id
where.0.indent = 0
where.0.operator = OperatorEquals
where.0.rowOperator = OperatorAnd
where.0.valueId = true
where.length = 1
```

### Grouping

The values can be grouped.

```crmscript
groups.0.fields.0.appendField = ticket.id
groups.0.fields.0.baseUrl = ?action=listTicket&id=
groups.0.fields.0.field = ticket.title
groups.0.fields.0.label = Title
groups.0.fields.1.appendField = ticket.id
groups.0.fields.1.baseUrl = ?action=listTicket&id=
groups.0.fields.1.field = ticket.owned_by.username
groups.0.fields.1.label = Owner
groups.0.fields.length = 2
groups.0.label = First
groups.length = 1
```

In this example, there's 1 group with 2 fields.

### HTML text with parser and database

Adds HTML-formatted text, including data from the database as [parser variables](@crmscript_parser).

This element also supports AJAX. See examples in the [element reference](@blogic_parser_code).

## Data table

A [data table](@blogic_data_table) adds a dynamic grid (table) **automatically filled with data**. The information is based on a query to the database.

### Example with simple values

```crmscript
criteria.0.field = ticket.(ticket_customers->ticket_id).customer_id.contact_id
criteria.0.indent = 0
criteria.0.operator = OperatorEquals
criteria.0.rowOperator = OperatorAnd
criteria.0.valueId = true
criteria.1.field = ticket.status
criteria.1.indent = 0
criteria.1.operator = OperatorLte
criteria.1.rowOperator = OperatorAnd
criteria.1.value = 3
criteria.length = 2
dbDistinct = true
distinct = ticket.id
profileElementName = ej_viewContact_ticketTable
```

### Example with callback script

In this example, the data table contains requests with ID less than 50. The table lists the title, the owner's username, and the status. The ID is a hidden field.

```crmscript
fields.0.field = ticket.title
fields.0.label = Title
fields.1.field = ticket.owned_by.username
fields.1.label = Owner
fields.2.field = ticket.id
fields.2.hidden = true
fields.3.field = ticket.status
fields.3.label = Status
fields.length = 4

criteria.0.field = ticket.id
criteria.0.indent = 0
criteria.0.operator = OperatorLt
criteria.0.rowOperator = OperatorAnd
criteria.0.value = 50
criteria.length = 1

showTicketStatus = true
url = ticket.exe?action=listTicket&ticketId=
```

Now, lets **change the colors** of the rows:

* We add a new hidden field to store the value of the colors. You can use any field not already in the table. Remember to update `fields.length`.
* Then we tie in a callback function `formatDisplayField()` to do the magic.

**Config:**

```crmscript
fields.4.hidden = true
fields.4.field = ticket.author
fields.length = 5

colorField = ticket.author
callbackInit = init
callbackDisplay = formatDisplayField
```

**Callback functions (in the Body tab):**

```crmscript
// Set up the SearchEngine
Void init(SearchEngine se) {
  se.addField("ticket.owned_by");
}

// Change the colorfield according to the ticket's status.
// Add a text on the owner's column for the users that have status not present.
// Translate status IDs to text.
String formatDisplayField(SearchEngine se, String field) {
  if(field == "ticket.owned_by.username") {
    User u;
    u.load(se.getField("ticket.owned_by").toInteger());
    if (u.getValue("status") == "2")
      return se.getField(field) + " : Not present";
    else
      return se.getField(field);
  }
  
  else if(field == "ticket.status") {
    if(se.getField("ticket.status").toInteger() == 1)
      return "Open";
    else if (se.getField("ticket.status").toInteger() == 2)
      return "Closed";
    else if (se.getField("ticket.status").toInteger() == 3)
      return "Postponed";
    else if (se.getField("ticket.status").toInteger() == 4)
      return "Deleted";
  }
  else if (field == "ticket.author") {
    if(se.getField("ticket.status").toInteger() == 1)
      return "#8888FF";
    else
      return "#FF8888";
  }
  // default, return the field unchanged
  return se.getField(field);
}
```

### Static grid

[Static grid](@blogic_static_grid) adds an empty static grid (table). You must add contents manually!

### Chart

[Chart](@blogic_chart) adds a chart using the JavaScript **charts** library.

## Context-specific elements

* [Dependency graph](@blogic_dependency_graph) (for project)

* [Messages](@blogic_messages): display the messages for a ticket

* [Recipients](@blogic_recipients): shows email recipients

* [Planner (diary)](@blogic_planner): shows a day schedule

## Scripts

* [ejScript](@blogic_ejscript): for the `body` config element

* [Ejscript element](@blogic_ejscript_element): a completely scriptable element