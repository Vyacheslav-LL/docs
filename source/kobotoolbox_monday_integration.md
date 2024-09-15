# KoboToolbox Integration on monday.com
**Last updated:** <a href="https://github.com/kobotoolbox/docs/blob/8c97f9358780418e9384e2ba5c99f466d6022b8d/source/kobotoolbox_monday_integration.md" class="reference">28 Aug 2023</a>

The KoboToolbox Integration allows users to easily synchronize their project
data from a KoboToolbox project to a monday.com board. In just a few steps you
can set up the integration to automatically copy data submissions received in
KoboToolbox to any of your monday.com boards. This integration significantly
reduces the manual work involved in copy-pasting project data between the two
platforms.

## Features

- Simplified process of connecting KoboToolbox projects with monday.com boards
- Easy mapping of monday.com fields to KoboToolbox questions using any label
  language defined in the form
- Real-time synchronization of newly created submissions to create new items

## Installation & First Use

### Prerequisites

1.  Create an account on KoboToolbox if you don't have one yet. Use this
    [guidance](https://support.kobotoolbox.org/creating_account.html) to set up
    your free account.
2.  Prepare a monday.com board mirroring the structure of your KoboToolbox
    project so that all fields from your KoboToolbox project are represented on
    a monday.com board.
3.  During the application setup of the integration, there is a need to
    authenticate access to your account by providing your KoboToolbox API token.
    To get your API token, use any of the methods described
    [here](https://support.kobotoolbox.org/api.html?highlight=api%20token).

### Installation

1.  Install the KoboToolbox integration from
    [monday.com apps marketplace](https://monday.com/marketplace).
2.  Once installed, go to your previously prepared board to set up the
    integration.
    Note: Only one KoboToolbox integration recipe can be established per monday board.

### First-time Use

1.  Go to the integration menu on the top right.
    ![monday-board-integrate](/images/kobotoolbox_monday_integration/monday-board-integrate.png)
2.  Find KoboToolbox in the Integrations Center.
    ![app-marketplace](/images/kobotoolbox_monday_integration/find-integration.png)
3.  Click on the integration and choose the included recipe.
    ![kobo-integration](/images/kobotoolbox_monday_integration/choose-recipe.png)
4.  On the next step authorize your KoboToolbox app into monday.com platform by providing the following data
    1. Select the appropriate server
    There are two KoboToolbox servers available: kobo.humanitarianresponse.info for humanitarian organizations, whereas kf.kobotoolbox.org is for everyone else.
    2. Provide your API key prepared earlier ![provide-api-key](/images/kobotoolbox_monday_integration/provide-api-key.png)  
    Note: In order to change the API key after the integration recipe setup, KoboToolbox Integration app should be completely reinstalled or user should delete all integrations installed by this user.
5. For recipe configuration, set up the following parameters
    1.  Choose the appropriate KoboToolbox project from the dropdown. Only
        deployed projects are available for selection
    2.  Choose the label language from the dropdown. If your form contains more
        than one language, select the one that should be used to map questions
        to columns. The selected language will only be displayed to map
        KoboToolbox questions with monday.com columns. The data displayed in the
        monday.com board will always use the underlying XML data structure
        instead of translated Select One or Select Multiple labels.
    3.  Click "Item" to set up the mapping of questions to columns .
        ![dynamic-linking](/images/kobotoolbox_monday_integration/item-mapping.png)
5.  Once you are done with the recipe configuration, click the "Add to Board"
    button. ![recipe](/images/kobotoolbox_monday_integration/recipe-config.png)
6.  Now that you have the integration in place, there is a last step to
    configure REST Server on the KoboToolbox side. This is required to tell your
    KoboToolbox project to automatically forward data to monday.com. To do that,
    execute the following steps:
    1.  Copy the integration link from the notification message sent to you on
        successful integration setup. The same link is added to the board
        description, so you can get it from there as well.\
        ![webhook-url](/images/kobotoolbox_monday_integration/description-link.png)
    2.  Log into your KoboToolbox account
    3.  Go to the appropriate project. Then open the Settings tab, choose REST
        Services, and click on 'Register a new service' button\
        ![create-rest-service](/images/kobotoolbox_monday_integration/create-rest-service.png)
    4.  Enter "monday.com integration" as the Service Name and paste the
        previously copied integration link in the "Endpoint URL" field.
    5.  In the "Custom HTTP Headers" section, insert the value "webhook-auth" in
        the "Name" field and put your Kobo API token in the "Value" field.\
        ![rest-service-modal](/images/kobotoolbox_monday_integration/rest-service-modal.png)
    6.  Click the 'Create' button.
7.  That's all! Now each new submission to the KoboToolbox project will be
    automatically be added to your monday.com board according to your recipe
    configuration.\

    ![kobo-monday-data](/images/kobotoolbox_monday_integration/kobo-monday-data.png)
    Notes: 
    1. Any updates made to a form or individual submission in KoboToolbox
    project which is already sent to monday.com board will not be automatically
    synced at this point. Such changes like removing or renaming a question,
    changing group hierarchy, changing a group to a repeat group, or editing
    labels in the KoboToolbox form will not affect the items on monday.com
    board.
    2. Due to monday.com limitations there is no way to map a column with Location type in the dynamic fields mapping. To overcome this limitation the following workflow should be established  
      a. Create two columns on monday.com board for location data to be populated - one of the Text type and second of the Location type. It’s important to name them identically. 
      b. Use a location column of the Text type in the dynamic fields mapping.  Second column of the Location type would be automatically populated once the first one is filled out.


## FAQ

**What is the REST Service?**

More information about REST Services could be found in the following
[guidance](https://support.kobotoolbox.org/rest_services.html).

**What is the dynamic fields mapping?**

Dynamic fields mapping is a pairing of fields represented on the monday.com
board with the appropriate questions from the KoboToolbox project.

**What happens if I change my data in the Kobo account?**

Any updates made to a form or individual submission in KoboToolbox project which
is already sent to monday.com board will not be automatically synced at this
point.

**What happens if I change my data on the monday.com board?**

Changes made to data represented on the monday.com board will not be reflected
in the KoboToolbox project.

**What happens if I need to later change the language?**

Language selection affects only the dynamic fields mapping view on integration
recipe configuration step. Board data will not be translated.

**What happens if I delete the board on Kobo?**

If a project is deleted in Kobo, the integration would not run until the
integration recipe is updated with a new project.

**How do multiple select questions on Kobo transfer to monday?**

For multi select questions a column with Dropdown type should be used on
monday.com board to have all selected options correctly transferred to the
board.

**How do single select questions on Kobo transfer to monday?**

For single select questions columns with Dropdown or Text types can be used to
have the selected option correctly transferred to the board.

**What column types from Kobo shift to what column types from monday?**

All column types except File and External XML are supported by monday.com. If
you can't find the appropriate column type on monday.com board, use a column
with Text type. For the Point and Area Kobo column type, it's better to use the Text
column on monday side despite the fact that there is Location column type for
this matter.

**Can I sync more than one KoboToolbox project with my monday board?**

No; only one KoboToolbox integration recipe can be established per board. 
Having more than one recipe will lead to a server error.
