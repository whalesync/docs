# Authorize Sanity

Whalesync connects to Sanity with an API token (Sanity calls these robot tokens). The token must have the **Editor** role so Whalesync can create, update, and delete documents.

1. Open [sanity.io/manage](https://www.sanity.io/manage) and choose your project.
2. Go to **API**, then **Tokens**, and click **Add API token**.
3. Name it, for example "Whalesync", and choose the **Editor** permission.
4. Copy the token. Sanity shows it only once.
5. Paste it into the **API token** box in Whalesync.

If the token can access more than one project, also enter the **Project ID**. You can find it on the project's page in sanity.io/manage. Most tokens are scoped to a single project, so this box can usually stay empty.

{% hint style="info" %}
Before Whalesync can list your document types, your Studio schema must be deployed to the dataset. Run `npx sanity schema deploy` in your Studio project. See [Sanity's guide to schema deployment](https://www.sanity.io/docs/apis-and-sdks/schema-deployment) and the [Sanity connector guide](README.md#before-you-connect-deploy-your-studio-schema).
{% endhint %}
