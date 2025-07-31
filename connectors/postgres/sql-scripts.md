---
description: Code to help you quickly create Postgres tables to sync with other apps
---

# SQL scripts

{% tabs %}
{% tab title="HubSpot" %}
```sql
CREATE TYPE crm_status AS ENUM (
	'Cold', 
	'Waitlist', 
	'Contacted', 
	'Meeting Complete', 
	'Should Follow Up', 
	'Paying Customer', 
	'Churned');

CREATE TABLE crm (
	id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
	"Contact Name" text,
	"Status" crm_status,
	"Email" text,
	"Company" text,
	"Title" text,
	"Source" text,
	"Twitter" text,
	"LinkedIn" text,
	"Personal Website" text,
	"VIP" boolean,
	"Enthusiasm (1-5)" integer
);

```
{% endtab %}

{% tab title="Shopify" %}
```sql
CREATE TYPE published_scope AS ENUM ('web', 'global');

CREATE TYPE sort_order AS ENUM ('alpha-asc', 'alpha-desc', 'best-selling', 'created', 'created-desc', 'manual', 'price-asc', 'price-desc');

CREATE TYPE state AS ENUM ('disabled', 'invited', 'enabled', 'declined');

CREATE TYPE status AS ENUM ('active', 'archived', 'draft');

CREATE TYPE tax_exemptions AS ENUM ('EXEMPT_ALL', 'CA_STATUS_CARD_EXEMPTION', 'CA_DIPLOMAT_EXEMPTION', 'CA_BC_RESELLER_EXEMPTION', 'CA_MB_RESELLER_EXEMPTION', 'CA_SK_RESELLER_EXEMPTION', 'CA_BC_COMMERCIAL_FISHERY_EXEMPTION', 'CA_MB_COMMERCIAL_FISHERY_EXEMPTION', 'CA_NS_COMMERCIAL_FISHERY_EXEMPTION', 'CA_PE_COMMERCIAL_FISHERY_EXEMPTION', 'CA_SK_COMMERCIAL_FISHERY_EXEMPTION', 'CA_BC_PRODUCTION_AND_MACHINERY_EXEMPTION', 'CA_SK_PRODUCTION_AND_MACHINERY_EXEMPTION', 'CA_BC_SUB_CONTRACTOR_EXEMPTION', 'CA_SK_SUB_CONTRACTOR_EXEMPTION', 'CA_BC_CONTRACTOR_EXEMPTION', 'CA_SK_CONTRACTOR_EXEMPTION', 'CA_ON_PURCHASE_EXEMPTION', 'CA_MB_FARMER_EXEMPTION', 'CA_NS_FARMER_EXEMPTION', 'CA_SK_FARMER_EXEMPTION');

CREATE TABLE public."Collects"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Collection" uuid,
"Created at" timestamp without time zone,
"Position" decimal,
"Product" uuid,
"Shopify Record ID" text,
"Updated at" timestamp without time zone
);

CREATE TABLE public."Custom Collections"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Description" text,
"Handle" text,
"Image" text,
"Published at" timestamp without time zone,
"Shopify Record ID" text,
"Sort order" sort_order,
"Title" text,
"Updated at" timestamp without time zone
);

CREATE TABLE public."Customers"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Addresses" text,
"Created at" timestamp without time zone,
"Default address" text,
"Email" text,
"Email marketing consent" text,
"First name" text,
"Last name" text,
"Last Order" text,
"Multipass identifier" decimal,
"Note" text,
"Orders count" decimal,
"Password" text,
"Password confirmation" text,
"Phone" text,
"Shopify Record ID" text,
"Sms marketing consent" text,
"State" state,
"Tax Exemption" boolean,
"Tax exemptions" tax_exemptions[],
"Total spent" decimal,
"Updated at" timestamp without time zone,
"Verified email" boolean
);

CREATE TABLE public."Images"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Created at" timestamp without time zone,
"Height" decimal,
"Image" text,
"Position" decimal,
"Shopify Record ID" text,
"Updated at" timestamp without time zone,
"Width" decimal
);

CREATE TABLE public."Options"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Name" text,
"Position" decimal,
"Shopify Record ID" text,
"Values" text[]
);

CREATE TABLE public."Products"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Created at" timestamp without time zone,
"Default Image" text,
"Description" text,
"Handle" text,
"Images_fk_Images" uuid[],
"Options_fk_Options" uuid[],
"Point of Sale" published_scope,
"Product type" text,
"Published at" timestamp without time zone,
"Shopify Record ID" text,
"Status" status,
"Tags" text[],
"Template suffix" text,
"Title" text,
"Updated at" timestamp without time zone,
"Variants_fk_Variants" uuid[],
"Vendor" text
);

CREATE TABLE public."Variants"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Barcode" text,
"Created at" timestamp without time zone,
"Image" uuid,
"Inventory quantity" decimal,
"Option 1" text,
"Option 2" text,
"Option 3" text,
"Position" decimal,
"Price" decimal,
"Shopify Record ID" text,
"Sku" text,
"Title" text,
"Updated at" timestamp without time zone,
"Weight (g)" decimal,
"Weight (lb)" decimal
);

ALTER TABLE public."Collects"
ADD CONSTRAINT collects_collection_custom_collections_fkey
FOREIGN KEY ("Collection")
REFERENCES public."Custom Collections"("id");

ALTER TABLE public."Collects"
ADD CONSTRAINT collects_product_products_fkey
FOREIGN KEY ("Product")
REFERENCES public."Products"("id");

ALTER TABLE public."Variants"
ADD CONSTRAINT variants_image_images_fkey
FOREIGN KEY ("Image")
REFERENCES public."Images"("id");
```
{% endtab %}

{% tab title="WordPress" %}
```sql
CREATE TYPE comment_status AS ENUM ('open', 'closed');

CREATE TYPE format AS ENUM ('standard', 'aside', 'chat', 'gallery', 'link', 'image', 'quote', 'status', 'video', 'audio');

CREATE TYPE media_type AS ENUM ('image', 'file');

CREATE TYPE ping_status AS ENUM ('open', 'closed');

CREATE TYPE status AS ENUM ('publish', 'future', 'draft', 'pending', 'private', 'acf-disabled', 'inherit');

CREATE TYPE taxonomy AS ENUM ('category', 'post_tag');

CREATE TABLE public."Categories"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Count" integer,
"Description" text,
"Link" text,
"Name" text,
"Slug" text,
"Taxonomy" taxonomy,
"WordPress.org Record ID" text
);

CREATE TABLE public."Media"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Alt text" text,
"Author" uuid,
"Caption" text,
"Comment status" comment_status,
"Date" timestamp without time zone,
"Description" text,
"Link" text,
"Media details" text,
"Media type" media_type,
"Mime type" text,
"Modified" timestamp without time zone,
"Ping status" ping_status,
"Slug" text,
"Source url" text,
"Status" status,
"Title" text,
"WordPress.org Record ID" text
);

CREATE TABLE public."Pages"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Author" uuid,
"Comment status" comment_status,
"Content" text,
"Date" timestamp without time zone,
"Excerpt" text,
"Featured media" uuid,
"Link" text,
"Menu order" integer,
"Modified" timestamp without time zone,
"Ping status" ping_status,
"Slug" text,
"Status" status,
"Title" text,
"WordPress.org Record ID" text
);

CREATE TABLE public."Posts"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Author" uuid,
"Categories" uuid,
"Comment status" comment_status,
"Content" text,
"Date" timestamp without time zone,
"Excerpt" text,
"Featured media" uuid,
"Format" format,
"Link" text,
"Modified" timestamp without time zone,
"Ping status" ping_status,
"Slug" text,
"Status" status,
"Sticky" boolean,
"Tags" uuid,
"Title" text,
"WordPress.org Record ID" text
);

CREATE TABLE public."Tags"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Count" integer,
"Description" text,
"Link" text,
"Name" text,
"Slug" text,
"Taxonomy" taxonomy,
"WordPress.org Record ID" text
);

CREATE TABLE public."Users"(
"id" uuid PRIMARY KEY DEFAULT gen_random_uuid(),
"Avatar urls" text,
"Description" text,
"Link" text,
"Name" text,
"Slug" text,
"Url" text,
"WordPress.org Record ID" text
);

ALTER TABLE public."Media"
ADD CONSTRAINT media_users_fkey
FOREIGN KEY ("Author")
REFERENCES public."Users"("id");

ALTER TABLE public."Pages"
ADD CONSTRAINT pages_media_fkey
FOREIGN KEY ("Featured media")
REFERENCES public."Media"("id");

ALTER TABLE public."Pages"
ADD CONSTRAINT pages_users_fkey
FOREIGN KEY ("Author")
REFERENCES public."Users"("id");

ALTER TABLE public."Posts"
ADD CONSTRAINT posts_categories_fkey
FOREIGN KEY ("Categories")
REFERENCES public."Categories"("id");

ALTER TABLE public."Posts"
ADD CONSTRAINT posts_media_fkey
FOREIGN KEY ("Featured media")
REFERENCES public."Media"("id");

ALTER TABLE public."Posts"
ADD CONSTRAINT posts_tags_fkey
FOREIGN KEY ("Tags")
REFERENCES public."Tags"("id");

ALTER TABLE public."Posts"
ADD CONSTRAINT posts_users_fkey
FOREIGN KEY ("Author")
REFERENCES public."Users"("id");
```
{% endtab %}
{% endtabs %}
