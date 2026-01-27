{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# Authorize Bubble

In order to connect Bubble to Whalesync, you'll need two things:

* Your Bubble app API key
* Your Bubble app API URL

### Setting up the Bubble Data API and getting your API key

In Bubble, go to Settings (1), then to the API tab (2). Check the box to enable the Data API (3).

<figure><img src="../../.gitbook/assets/image (6).png" alt="Screenshot of the Bubble API settings page"><figcaption><p>Bubble API settings</p></figcaption></figure>

Your data types will show up right below. Check the box for every data type that you want to sync, to enable the API for that type.

<figure><img src="../../.gitbook/assets/image (5).png" alt="Screenshot of the Bubble API settings page data types"><figcaption><p>Bubble data types exposed via the API</p></figcaption></figure>

{% hint style="danger" %}
**Keep "use field display instead of ID for key names" unchecked**\
One more important thing: we strongly recommend making sure that "Use field display instead of ID for key names" is OFF (unchecked). That setting can break your syncing if any type or field names in Bubble are changed.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (30).png" alt="Screenshot of the Bubble API settings page with the &#x22;Use field display instead of ID for key names&#x22; option unchecked"><figcaption><p>Please uncheck "Use field display instead of ID for key names"</p></figcaption></figure>

Now you can grab your API key. Look below in the API tokens section. If you already have a token, you can use that. Or, click "Generate a new API token" (1). Then copy the "Private key" (2).

<figure><img src="../../.gitbook/assets/image (29).png" alt="Screenshot of the Bubble API settings page with the API key"><figcaption><p>API key</p></figcaption></figure>

### Getting your Bubble Data API URL

Make sure the settings changes you made in the previous step are published to your live Bubble app. Then, change your view using the menu in the top right, switching from "Development" to "Live" version.

{% hint style="danger" %}
**Warning**: The URL is different if you're looking at the "Development" version of your app and includes an extra "/version-test". Unless you're just testing things, you will likely want to use the production URL without the extra "/version-test".
{% endhint %}

Copy the "Data API root URL" value.

<figure><img src="../../.gitbook/assets/image (21).png" alt="Screenshot of the Bubble API settings page with the API URL"><figcaption><p>Data API root URL</p></figcaption></figure>
