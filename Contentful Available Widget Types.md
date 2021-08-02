---
date: 2021-06-22
title: Contentful Available Widget Types 
publish: true
slug: /dev/contentful/available-widget-types
tags:
  -
---

Relates to: [[Contentful|61.04.01 Contentful]]

| Widget ID          | Applicable field type         | Description                                                                                                         |
| ------------------ | ----------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| assetLinkEditor    | Asset                         | Search, attach, and preview an asset.                                                                               |
| assetLinksEditor   | Asset (array)                 | Search, attach, reorder, and preview multiple assets.                                                               |
| assetGalleryEditor | Asset (array)                 | Search, attach, reorder, and preview multiple assets in a gallery layout                                            |
| boolean            | Boolean                       | Radio buttons with customizable labels.                                                                             |
| datePicker         | Date                          | Select date, time, and timezon.                                                                                     |
| entryLinkEditor    | Entry                         | Search and attach another entry.                                                                                    |
| entryLinksEditor   | Entry (array)                 | Search and attach multiple entries.                                                                                 |
| entryCardEditor    | Entry                         | Search, attach, and preview another entry.                                                                          |
| entryCardsEditor   | Entry (array)                 | Search, attach and preview multiple entries.                                                                        |
| numberEditor       | Integer, Number               | A simple input for numbers.                                                                                         |
| rating             | Integer, Number               | Uses stars to select a number.                                                                                      |
| locationEditor     | Location                      | A map to select or find coordinates from an address.                                                                |
| objectEditor       | Object                        | A code editor for JSON                                                                                              |
| urlEditor          | Symbol                        | A text input that also shows a preview of the given URL.                                                            |
| slugEditor         | Symbol                        | Automatically generates a slug and validates its uniqueness across entries.                                         |
| listInput          | Symbol (array)                | Text input that splits values on `,` and stores them as an array.                                                   |
| checkbox           | Symbol (array)                | A group of checkboxes. One for each value from the `in` validation on the content type field                        |
| tagEditor          | Symbol (array)                | A text input to add a string to the list. Shows the items as tags and allows to remove them.                        |
| multipleLine       | Text                          | A simple `<textarea>` input                                                                                         |
| markdown           | Text                          | A full-fledged [markdown editor](https://www.contentful.com/r/knowledgebase/markdown/)                              |
| singleLine         | Text, Symbol                  | A simple text input field                                                                                           |
| dropdown           | Text, Symbol, Integer, Number | A `<input type="select">` element. It uses the values from an `in` validation on the content type field as options. |
| radio              | Text, Symbol, Integer, Number | A group of radio buttons. One for each value from the `in` validation on the content type field                     |
| richTextEditor     | richTextEditor                | A default rich text editor                                                                                                                    |
