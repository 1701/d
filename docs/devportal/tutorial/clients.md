# netID Clients

## Creating a Client 

Create a Client for this service by clicking on Client hinzufügen (Add client). 
Detailed documation on how to do this is available in the netID Developer Portal. 

Sample configuration:

![netid](../../images/netid_create-client-sample.png)

!!! alert ""
    Note: the values here should be adjusted to your needs, especially "Callback URL", which needs to point to your backend

In the end, it should look similar to this:

![netid](../../images/netid_create-client-02-new.png)

Once the client is created it will initially run in a sandboxed mode, which means it can only be used with whitelisted netID-Accounts (email addresses).

In order to successfully run through the initial integration add a test user (email address) to the whitelist by selecting **Add Test-Account**, 
outlined on the developer portal. Up to 10 accounts can be whitelisted per sandboxed client.

Finally, find the **Client ID** and **netID Token - Sandbox** (later referred to as **client secret**) by expanding the client details. 

![netid](../../images/netid_client-details-01-new.png)


## Edit a Client

1. Under the appropriate service, select the client to be changed.
2. Click **Edit** next to the Client name.

A text box will appear asking you to confirm the operation with your password.

3. Enter the password that you created during the registration in the netID Developer Portal and confirm your entry by clicking on **Confirm**.
   
You now have the possibility to change the entered information about the Client.

4. Make the desired changes and updates and save the information with a click on **Update Client**.

!!! success ""
    The client was successfully changed.

## Deactivate a Client

1. Under the appropriate service, select the client to be disabled.
2. Click **Edit** next to the Client name.

A text box will appear asking you to confirm the operation with your password.

3. Enter the password you created for logging into the netID Developer Portal and confirm your entry by clicking on **Confirm**.

You now have the possibility to change the status of the Client.

4. To deactivate the client, select the entry Inactive in the drop down menu under Status.

!!! success ""
    The client was successfully deactivated.

!!! info ""
    You have the possibility to [reactivate the client](#reactivate-a-client) within 14 days before it is finally deleted and removed from the overview.

## Delete a Client

1. Under the appropriate service, select the client to be removed.
2. Click the arrow next to the Client name to expand the entire Client.
3. Click **Delete Client** below.

A text box will appear asking you to confirm the operation with your password.

4. Enter the password that you created during the registration in the netID Developer Portal and confirm your entry by clicking on **Confirm**.

!!! success ""
    The client has been deleted. The status of the deleted client is set to DELETE.

!!! info ""
    You have the possibility to reactivate the client within 14 days before it is finally deleted and removed from the overview.

## Reactivate a Client

A deactivated client remains in the overview. The status of the deleted client is set to DELETE. This gives you the opportunity to reactivate a deactivated client within 14 days before it is finally deleted and removed from the overview.

1. Under the appropriate service, select the client to be reactivated.
2. Click the arrow next to the Client name to expand the entire Client.
3. Click **Reactivate Client** under the Client Status.
4. To finally reactivate the client, confirm the process with your developer account password.

!!! success ""
    The client has been reactivated. The status is now displayed again as ACTIVE.