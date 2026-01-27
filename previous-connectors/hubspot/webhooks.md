---
description: >-
  Info on which properties HubSpot supports webhooks for and how that impacts
  syncing
---

{% hint style="warning" %}
**Archived:** This connector is no longer offered by Whalesync. Existing syncs will continue to run, but future improvements and support will be limited. See [Previous Connectors](../) for more details.
{% endhint %}

# Webhooks

## FAQ

### When does Whalesync use webhooks?

* Whalesync uses webhooks whenever possible to offer instant syncing.
* HubSpot supports webhooks for many of its properties but not _all_ of them.

### What happens when HubSpot doesn't offer webhooks?

* Whalesync relies on polling to detect changes when HubSpot doesn't offer webhooks.
* Polling happens once every 3 hours.

### All together, how fast will Whalesync sync changes in HubSpot?

* Changes in any of the webhook-supported properties below will be detected within seconds.
* Changes in properties HubSpot does not offer webhooks for will be detected once every 3 hours.



## Properties with Webhooks

Below is a list of properties for which HubSpot supports webhooks:

{% tabs %}
{% tab title="Contacts" %}
```
firstname 
lastname 
email 
mobilephone 
address 
zip 
message 
website 
twitterhandle 
hs_analytics_source 
hs_persona 
followercount 
industry 
annualrevenue 
numemployees 
lifecyclestage 
closedate 
company 
jobtitle 
hs_language 
country 
city 
fax 
state 
twitterprofilephoto 
hs_legal_basis 
salutation 
phone 
hs_content_membership_notes 
hs_content_membership_status 
hs_buying_role 
hs_lead_status 
hubspot_owner_id 
owneremail 
ownername 
hs_all_assigned_business_unit_ids 
hs_content_membership_email 
hs_country_region_code 
hs_journey_stage 
hs_role 
hs_seniority 
hs_shared_team_ids 
hs_shared_user_ids 
hs_state_code 
hs_sub_role 
hs_time_between_contact_creation_and_deal_close 
hs_time_between_contact_creation_and_deal_creation 
hs_time_to_move_from_lead_to_customer 
hs_time_to_move_from_marketingqualifiedlead_to_customer 
hs_time_to_move_from_opportunity_to_customer 
hs_time_to_move_from_salesqualifiedlead_to_customer 
hs_time_to_move_from_subscriber_to_customer 
hs_timezone 
hs_whatsapp_phone_number 
hs_linkedin_url 
linkedinbio 
linkedinconnections 
twitterbio 
hs_latest_source 
hs_latest_source_timestamp 
hs_facebook_click_id 
hs_google_click_id 
hs_email_customer_quarantined_reason 
company_size 
date_of_birth 
degree 
field_of_study 
gender 
graduation_date 
job_function 
marital_status 
military_status 
relationship_status 
school 
seniority 
start_date 
kloutscoregeneral 
work_email 
```
{% endtab %}

{% tab title="Companies" %}
```
name 
phone 
city 
zip 
numberofemployees 
lifecyclestage 
description 
web_technologies 
twitterfollowers 
linkedinbio 
hs_analytics_source 
facebookfans 
timezone 
founded_year 
linkedin_company_page 
facebook_company_page 
twitterbio 
twitterhandle 
type 
hs_lead_status 
annualrevenue 
closedate 
industry 
domain 
website 
country 
state 
address2 
googleplus_page 
about_us 
address 
total_money_raised 
hubspot_owner_id 
hs_all_assigned_business_unit_ids 
hs_country_code 
hs_csm_sentiment 
hs_employee_range 
hs_industry_group 
hs_keywords 
hs_linkedin_handle 
hs_logo_url 
hs_quick_context 
hs_revenue_range 
hs_shared_team_ids 
hs_shared_user_ids 
owneremail 
ownername 
hs_ideal_customer_profile
```
{% endtab %}

{% tab title="Deals" %}
```
dealname 
amount 
closedate 
dealtype 
closed_lost_reason 
closed_won_reason 
description 
createdate 
deal_currency_code 
hs_analytics_source 
dealstage 
pipeline 
hs_exchange_rate 
ecosystem_trx_refunded_at 
hs_all_assigned_business_unit_ids 
hs_deal_stage_probability 
hs_forecast_probability 
hs_manual_forecast_category 
hs_next_step 
hs_priority 
hs_shared_team_ids 
hs_shared_user_ids 
hubspot_owner_id 
```
{% endtab %}

{% tab title="Tickets" %}
```

subject changed
content changed
source_type changed
hs_resolution changed
createdate changed
hs_ticket_priority changed
hs_pipeline changed
hs_pipeline_stage changed
hs_ticket_category changed
closed_date changed
hs_file_upload changed
hs_last_closed_date changed
hs_all_assigned_business_unit_ids changed
hs_shared_team_ids changed
hs_shared_user_ids changed
hs_time_to_close_in_operating_hours changed
hs_time_to_first_response_in_operating_hours changed
hubspot_owner_id changed
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Webhooks are **not** supported for _custom properties_. You can sync custom properties with Whalesync, but changes will only be detected during polling.
{% endhint %}

