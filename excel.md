# Excel

A cheatsheet for Excel, because although it's mostly straightforward, most people don't take the time to go in depth to learn all the functionality it has.

## Formulas

Every formula has the following 3 parts:

`= Function Name (Arguments)`

Evaluate Formulas: This is a great tool to debug formulas. It's similar to code debugging where you can step in to a formula and see at each step what a formula returns. This can be found at `Formulas` > `Formula Auditing` > `Evaluate Formulas`.

Function Name | Description | Example
------------- | ----------- | -------
[SUM](https://support.microsoft.com/en-us/office/sum-function-043e1c7d-7726-4e80-8f32-07b23e057f89) | The SUM function adds values. You can add individual values, cell references or ranges or a mix of all three. | `=SUM(A2:A10)` Adds the values in cells A2:10. |
[MIN](#) | awef | asdfafd

## Shortcuts

For the most up to date shortcuts, refer to Microsoft's [help article](https://support.microsoft.com/en-us/office/keyboard-shortcuts-in-excel-1798d9d5-842a-42b8-9c99-9b7213f0040). This table will list out shortcuts that I find useful.

Functionality | Shortcut
------------- | --------
AutoSum | `Alt + =`
Select the column | `Ctrl + Spacebar`
Select the row | `Shift + Spacebar`
Add new row or column | `Ctrl + Shift + Plus Sign (+)`
Remove a row or column | `Crtl + -`

## References

Relative Reference: Based on a specific location.

Absolute Reference:

`=E4/$E$9 * 100`

## Conditional Formatting

1. Highlight the cells.
2. Home > Styles > Conditional Formatting

## Data Visualization

Pie charts are good for a single column or row.

## Custom Sorts

If you have a column with the month spelled out, if you sort it ASC it will make it alphabetical. Excel has a built-in way to support sorting on the actual month values though.

1. Go to Data > Sort & Filter > Sort
2. Under Order click on "Custom List..."
3. Select the custom list.
4. Select the applicable list.

## Subtotal

The Subtotal command allows you to automatically create groups and use common functions like SUM, COUNT, and AVERAGE to help summarize your data. For example, the Subtotal command could help to calculate the cost of office supplies by type from a large inventory order. It will create a hierarchy of groups, known as an outline, to help organize your worksheet.

https://edu.gcfglobal.org/en/excel2016/groups-and-subtotals/1/

Go to Data > Subtotal.