{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# Authorize Shopify

## How to get your access token

#### 1. Go to App and sales channel settings

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/96630f45-4f16-40ad-9232-c9f901445fc3/b2a30be6-32e3-4789-aba4-2edf55db9bb2.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.5000&#x26;fp-y=0.5000&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=327&#x26;mark-y=251&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz01MjQmaD0zNSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw" alt=""><figcaption></figcaption></figure>

#### 2. Click on Develop apps

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/53cc4af1-fc16-403b-8144-954d450647d4/6724fdef-12db-4bcc-89d9-86d40622a9cc.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.5000&#x26;fp-y=0.5000&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=853&#x26;mark-y=91&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz05NSZoPTM1JmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D" alt=""><figcaption></figcaption></figure>

#### 3. Create your app

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/98624e57-6f76-44ee-89d5-80cb7da73094/7de4b427-f4e8-4d00-ace0-74f2944bdcc2.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.5000&#x26;fp-y=0.5000&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=364&#x26;mark-y=326&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00NzQmaD0zNSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw" alt=""><figcaption></figcaption></figure>

#### 4. Configure Admin API scopes

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/6659a590-7d35-4e65-b750-703f09b5a850/343251e4-ef35-4143-8389-2f4f0cce9221.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.5000&#x26;fp-y=0.5000&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=394&#x26;mark-y=382&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0xNzMmaD0zMCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw" alt=""><figcaption></figcaption></figure>

#### 5. Make sure to check read and write products

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/0082e259-378c-40b4-92b3-9241feb960b5/a4bf67c8-f43d-4e32-967d-1b4a2f98a2e8.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.5012&#x26;fp-y=0.6953&#x26;fp-z=2.2320&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=100&#x26;mark-y=357&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0xMDAyJmg9MjU5JmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D" alt=""><figcaption></figcaption></figure>

#### 6. Install your app

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/01b9dce5-677d-4d46-8ef3-376b83c2b273/b89dcb52-cc5a-44c3-8269-25d2a69366ec.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.5000&#x26;fp-y=0.5000&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=994&#x26;mark-y=91&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NSZoPTM1JmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D" alt=""><figcaption></figcaption></figure>

#### 7. Copy your Access token!

<figure><img src="https://images.tango.us/workflows/bc8daaac-834b-4df3-a66d-a1010968825a/steps/b073da90-5b47-4aed-9b35-6b56b64d1a27/5db75d97-3786-4cf2-aa55-571fafef6e75.png?fm=png&#x26;crop=focalpoint&#x26;fit=crop&#x26;fp-x=0.4631&#x26;fp-y=0.5736&#x26;fp-z=1.7561&#x26;w=1200&#x26;border=2%2CF4F2F7&#x26;border-radius=8%2C8%2C8%2C8&#x26;border-radius-inner=8%2C8%2C8%2C8&#x26;blend-align=bottom&#x26;blend-mode=normal&#x26;blend-x=0&#x26;blend-w=1200&#x26;blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&#x26;mark-x=316&#x26;mark-y=362&#x26;m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz01NjgmaD02MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw" alt=""><figcaption></figcaption></figure>



## How to get your store name

1\) Go to [https://accounts.shopify.com/store-login](https://accounts.shopify.com/store-login)

2\) Copy the values _before_ ".my.shopify.com"

e.g. our store name = "whalesync"

<figure><img src="../../.gitbook/assets/CleanShot 2023-06-26 at 15.36.00.png" alt=""><figcaption></figcaption></figure>

