
/*
*@author                         Muli Mutisya
*@author_email              writetomuli@gmail.com
*@Component                Joomla Donation Component powered by PesaPal
*@date                            12th January 2020
*/

Contents
⦁	Installation
⦁	Setup
⦁	Functionality
⦁	Approach

1.Installation
Having Joomla installed, follow the steps below;
Open admin of your Joomla installation
Under the Extensions menu , click Manage and then select install
Using the upload tool provided, upload this zip file (pesapal_task) which will install the component extension

2.Setup
On the Components menu at the admin end of your installation, click on the Donations - Pesapal component. This only appears after you install the component
Enter your Pesapal Consumer Key and Consumer Secret. To find out more about these, go to this link https://demo.pesapal.com
      2.1 Menu item setup
 From admin dashboard, click on menu and select All Menu items.
Select New and set up your menu details. 
On the Menu Item Type field, click on it and select Pesapal Donation and select the     Pesapal Donation item with the description 'Accept donations using Pesapal'
Assign your menu item to a menu and Save.
You can now start accepting donations via site powered by Pesapal. 
Click on the menu item created from the frontend.

3. Functionality
Collection of donation details from name, email, phone, donation amount, description and time period.
A payment can be made through pesapal using the details collected above.
An email notification is sent to donor (using the email submitted via the form) with a link to complete the payment.
An admin dashboard with all donation made and the status of each.


4. Approach
    4.1 Introduction 
I used the Model-View-Controller approach.
To learn more about MVC, use this link https://docs.joomla.org/J1.5:Developing_a_MVC_Component/Introduction
    4.2 Frontend/ Donation  view
This is where the form that collects donation details is displayed, where the iFrame is displayed on form submission and where a donor is able to complete a payment after they click on the link in the email.
Upon submission of the form a new donation record is created in the database.
An email is also sent using the Elastic Mail API - https://elasticemail.com (I used this to make sure emails are delivered no matter the server Joomla! is installed. Works as long as CURL is enabled). 
To generate the iframe, the OAuth.php class provided on the Pesapal Samples & Downloads section of the Developer site is used. It is also used on Callback.
When a user clicks on the link they receive via email, the donations model looks for the reference code from the url. If it is found, the donation with that code is fetched then it's details are used to generate the iframe. If not, the default form is displayed.
    4.3 Callback  view
Upon completion of a payment, the user is directed to this view.
The payment status is checked and the database is updated accordingly.
     4.4 Admin view
Data from the database is pulled via the model and is displayed using the template provided.



