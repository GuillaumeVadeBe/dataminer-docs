---
uid: DashboardTable
---

# Table

This component is used to display the results of queries in table format. It should always be configured with *Queries* data input. See [Creating a GQI query](xref:Creating_GQI_query).

![Table component](~/user-guide/images/Table_Component.png)<br>*Table component in DataMiner 10.4.1*

It displays the different possible data sources of queries as follows:

- Elements are represented with a row for each element, with each column detailing different information for that element.

- Services are displayed in the same way as elements.

- Table parameters are displayed as they are, as determined by the applied operators.

- If parameters are retrieved by protocol or profile definition, each row will represent a matching element, and for each parameter a column will show the corresponding values.

> [!NOTE]
>
> - From DataMiner 10.2.7/10.3.0 onwards, users can copy a cell, a column, a row, or the entire table via the right-click menu of the component. Unless a single cell is copied, the copy is in CSV format. If an entire column or single cell is copied, the values will not be encapsulated in double quotes. Copying an entire row or table will encapsulate all values in accordance with CSV formatting. If a value contains a double quote, this will be escaped when it is copied.
> - Prior to DataMiner 10.3.7/10.4.0, if the data in the table is fetched again by means of a [trigger component](xref:DashboardTrigger) or a [component action](xref:LowCodeApps_event_config) while data is selected in the table, this selection is lost. From DataMiner 10.3.7/10.4.0 onwards, the component will try to reapply the selection. This means that the table will keep fetching more data until all previously selected rows are found. When a previously selected row is missing, the table will fetch all data looking for it. Reapplying the previous selection will take precedence over selecting the first row when the *Initial Selection* setting is enabled. The table will also update its data to reflect the new selection. <!-- RN 36372 -->

> [!TIP]
> See also: [Tutorial: Creating a parameter table connected to an element feed](xref:Creating_a_parameter_table_connected_to_an_element_feed)

## Configuring the layout

You can **resize the columns** of the table by dragging the edges of the column headers. From DataMiner 10.1.8/10.2.0 onwards, you can also change the order of the columns by dragging the column headers to a different position.

> [!TIP]
> From DataMiner 10.4.1/10.5.0 onwards<!--RN 37522-->, you can adjust the default column width by accessing the [Template Editor](xref:Template_Editor) through *Layout > Column appearance*.

### Filtering & highlighting

In the *Layout* pane for this component, the *Conditional coloring* option is available, which allows you to highlight cells based on a condition. You can configure this option as follows:

- If the column you want to use for highlighting contains values for which a specific range can be specified, select the column, indicate the range to be highlighted, select the range and then click the color icon on the right to specify a highlight color. Multiple ranges can be indicated for one column, each with a color of its own.

- Alternatively, from DataMiner 10.2.0/10.1.8 onwards, you can filter on specific text instead. To do so, select the column you want to use for highlighting, specify the text, and select the highlight color. By default, the cell value will need to be equal to the specified text to be highlighted. However, you can change this by clicking *equal* above the text box and selecting *contain* or *match regex* instead, depending on the type of filtering you want to apply. You can also apply a negative filter by clicking *does*, which will make this field switch to *does not* instead.

- Multiple filters can be applied on the same value. In that case, the filters will be applied from the top of the list to the bottom. Positive filters will get priority over negative filters.

- You can remove a column filter again by selecting *No color* instead of a specific color.

From DataMiner 10.3.0 [CU20]/10.4.0 [CU8]/10.4.11 onwards<!--RN 40818-->, the *Show quick filter* setting allows you to determine whether the search box, which lets you [apply a general filter](#filtering-and-sorting-the-table) across the table, appears when you hover over the table component. This setting is enabled by default.

### Column appearance

From DataMiner 10.4.1/10.5.0 onwards<!-- RN 37522 -->, in the *Layout* pane, the *Column appearance* option is available, which allows you to customize the appearance of a column.

- To use one of the available presets to alter the column appearance, click the preview below the column name and select a preset option:

  - **Left**: The text is displayed on the left side of the column cell. This is the default setting for columns containing values of type string.

  - **Center**: The text is displayed in the center of the column cell.

  - **Right**: The text is displayed on the right side of the column cell. This is the default setting for columns containing values of type double or datetime.

  - **Hyperlink**: Only available for DataMiner Low-Code Apps. The text functions as a hyperlink, redirecting users to a new webpage in a separate tab.

    > [!NOTE]
    > If you select this preset option, a [*Navigate to a URL* action](xref:LowCodeApps_event_config#navigating-to-a-url) is automatically configured. The default URL is `https://[Your DMA]/{DMA root}`, which you can edit in the [Template Editor](xref:Template_Editor).

  - **Icon**: An icon is displayed in the center of the column cell. By default, the info icon is used.

  - **Background**: A background color is added to the column cell. By default, a blue color (#1F68BF) is used.

- To freely customize the appearance of a column, click the ellipsis button ("...") next to the column name and select *Customize preset* to open the Template Editor.

  > [!TIP]
  > For more information on using the Template Editor, see [Template Editor](xref:Template_Editor).

- If you open the Template Editor after selecting a preset option, the template may already contain certain configured layers.

  For example, if you selected the *Hyperlink* preset, a rectangle layer with opacity 0%, including a *Navigate to a URL* action, will be configured. Additionally, the text color of the text layer will be set to blue (#1F68BF), and the text inside the text box will be enclosed by HTML `<u>` elements to define underlined text.

- From DataMiner 10.4.0 [CU13]/10.5.0 [CU1]/10.5.4 onwards<!--RN 42226-->, you can reuse saved templates for components in the same dashboard or low-code app by clicking the ellipsis button ("...") next to the column name and selecting *Browse templates*.

## Adding actions to a table

If you add a table component to a custom app using the [DataMiner Low-Code Apps](xref:Application_framework), you can also configure actions for the component. This feature is not available in the Dashboards app. <!-- RN 29394 -->

To configure actions:

- From DataMiner 10.4.1/10.5.0 onwards<!--RN 37522-->:

  - In the Template Editor, you can **configure actions for table columns**. Actions can be linked to the *On click* event of a shape in a column template, allowing you to define your own links or buttons inside a table.

    > [!TIP]
    > For more information, see [Changing template settings](xref:Template_Editor#changing-template-settings).

  - You can also **configure actions that are executed when a row is double-clicked**:

    1. In the *Component > Settings* pane, expand the *Actions* section.

    1. Click *On double-click*.

    1. In the pop-up window, select the action that should be executed. See [Configuring low-code app events](xref:LowCodeApps_event_config).

- Prior to DataMiner 10.4.1/10.5.0:

  1. In the *Component* \> *Settings* pane, expand the *Actions* section.

  1. Click *Add action*.

  1. To specify how the action is triggered, at the top of the action configuration section, click the icon for text hyperlink, row double-click, or cell button.

  1. In the *Label* box, specify a label for the action.

  1. In the *Icon* box, select an icon for the action.

  1. In the *Action* box, select the action that should be executed. You can for instance use this to add an update action to the table, or to allow users to select an item or clear their selection. See [Configuring low-code app events](xref:LowCodeApps_event_config).

## Configuring other component settings

In the *Settings* pane for this component, you can customize its behavior to suit your requirements.

- If you want the data in the table to be refreshed automatically (provided this is supported by the data source), Set *Update data* to *On*. Note that while this setting is available from DataMiner 10.2.0/10.2.1 onwards<!-- RN 31450 -->, in older DataMiner versions it can only be used with the *Get parameter table by ID* query data source. From DataMiner 10.3.10/10.4.0 onwards<!-- RN 36789 -->, other data sources are also supported.

- If you want the first row to be selected by default, in the *Settings* pane, under *Initial Selection*, set the toggle button to *On* (available from DataMiner 10.3.6/10.4.0 onwards<!-- RN 35984 -->). This way, the first row will be automatically selected whenever the component is loaded or when the data in the table is refreshed.

- If you want to configure the message shown when a query returns no results, in the *Layout* pane, under *Advanced*, change the *Empty result message* setting to your custom message (available from 10.3.11/10.4.0 onwards<!-- RN 37173 -->). By default, this message is set to *Nothing to show*.

  > [!TIP]
  > See also: [Displaying a custom empty component message](xref:Tutorial_Dashboards_Displaying_a_custom_empty_component_message).

## Exporting the table

From DataMiner 10.1.3/10.2.0 onwards, you can export the content of the table by clicking the ... button in the top-right corner of the component and selecting *Export to CSV*. What happens next depends on your DataMiner version:

- Prior to DataMiner 10.3.8/10.4.0, if nothing is selected in the table, the entire table will be exported; otherwise only the selected rows will be exported. The data will contain the display values, not the raw values. This means that units will be included for the parameter values and that discrete values will be replaced by their corresponding display values.

- From DataMiner 10.3.8/10.4.0 onwards, a pop-up window will open where you can select whether the raw values or the display values from the table should be exported. Exporting the display values will result in a CSV file that contains all the values as they are seen in the table, formatted and with units. If you export the raw values, no formatting will be applied to them. The only exception are discrete values, for which the corresponding display values will always be exported. If no rows are selected in the table, the entire table will be exported; otherwise only the selected rows will be exported.

The export file will be named “Query XXX” (XXX being the name of the query, as configured in the *Data* pane). The first line of the CSV file will contain the names of the columns. The subsequent lines will contain the data, each line being a row of the query result.

> [!NOTE]
> To only export specific columns, first apply a filter by dragging the columns onto the table component before you export the component.

## Filtering and sorting the table

From DataMiner 10.2.7/10.3.0 onwards, users can filter and sort the contents of a table component in a dashboard.

> [!TIP]
> If you have made changes to the way a table is displayed, and you want to quickly reset your changes and return to the initial table view, click the eye icon in the top-right corner of the component (available from DataMiner 10.2.11/10.3.0 onwards).

### General filter

To apply a general filter across the table, a search box is available:

1. Hover over the table component and click the search icon.

1. Specify the filter text (case-insensitive) in the search box.

   This will apply a client-side filter only. To apply a server-side filter, you need to use a filter operator when you [configure the query data source](xref:Creating_GQI_query).

> [!IMPORTANT]
> From DataMiner 10.3.0 [CU20]/10.4.0 [CU8]/10.4.11 onwards<!-- RN 40818-->, the search box is only available when the [*Show quick filter* setting](#filtering--highlighting) is enabled.

### Column-based filter

To apply a filter based on a specific column:

1. Right-click the column header and select *Filter*.

1. Configure the different fields of the filter, depending on the type of value in the column.

   - For string values or GUIDs:

     - To switch between a positive or negative filter, click *does* or *does not*.

     - To switch to a different type of filter, click the second filter field. This will toggle between *contain*, *equal*, and *match regex*.

     - In the third field of the filter, specify a filter value.

   - For numeric or datetime values, specify the range that a value should be in.

   - For booleans, specify whether the value should be true or false.

   - For discrete values, from DataMiner 10.2.10/10.3.0 onwards, select the relevant checkboxes.

   > [!NOTE]
   > Prior to DataMiner 10.2.9/10.3.0, it is possible to specify multiple conditions by clicking the + icon. As soon as one of the specified conditions applies, a value will be shown (i.e. conditions are combined using "OR"). DataMiner 10.2.9/10.3.0 switches to more efficient server-side filtering, which greatly improves the filter performance but does not allow multiple conditions in the same filter.

1. Click *Apply filter*.

> [!NOTE]
> If you apply several column filters or apply both the general filter and one or more column filters, values will only be shown if they match all filters (i.e. filters are combined using "AND").

### Filter based on text string

From DataMiner 10.3.0 [CU20]/10.4.0 [CU8]/10.4.11 onwards<!--RN 40793-->, you can filter the table by passing it a text string.

You can do this in several different ways, for example:

- Use a **text input** or **search input** component:

  1. Add a [text input](xref:DashboardTextInput) or [search input](xref:DashboardSearchInput) component to your dashboard or app.

  1. Hover over the table component, click the filter icon, and then add a filter from the *Components > Text input #/Search input # > Value > Texts* section of the *Data* pane. Prior to DataMiner 10.3.0 [CU21]/10.4.0 [CU9]/10.4.12<!--RN 41075 + 41141-->, add a filter from the *Feeds > Text input #/Search input # > Value > Strings* section of the *Data* pane.

  When you input text in the published version of the dashboard or app, the table component will automatically filter based on this input, and the value will appear in the table's search box.

  > [!NOTE]
  > If you do not want the search box to appear when using text or search input data as a filter, disable the [*Show quick filter* setting](#filtering--highlighting) in the *Layout* pane.

  ![Text input](~/user-guide/images/Text_input_filter_table.gif)<br>*Text input and table components in DataMiner 10.4.11*

- Specify a **text string in the dashboard or app URL**:

  1. Hover over the component, click the filter icon, and then add a filter from the *URL > Text* section of the *Data* pane. Prior to DataMiner 10.3.0 [CU21]/10.4.0 [CU9]/10.4.12<!--RN 41075 + 41141-->, add a filter from the *Feeds > URL > Strings* section of the *Data* pane.

  1. Pass a string data object within the URL, as explained in [Specifying data input in a dashboard or app URL](xref:Specifying_data_input_in_a_URL).

     This URL will automatically display a filtered version of the table when the dashboard or app is opened.

     In the following example, the text string "test" is sent to the component with component ID 1:

     `https://<dma>/<app-id>?data={"components": [{"cid":1, "select":{"strings": ["test"]}}]`

### Sorting

To sort the table, you can **click a column header**. To toggle between ascending and descending order, click the column header again.

To apply **additional sorting**, press **Ctrl** while clicking one or more additional headers. The first column will then be used for the initial sorting, the next one to sort equal values of the first column, and so on.

Alternatively, you can also select one of the available sorting options in the **column header right-click menu**.

To **group** by a specific table column, right-click the column header and click *Group*. To stop grouping, right-click the header again and select *Stop grouping*.
