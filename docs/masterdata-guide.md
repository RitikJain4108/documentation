# Masterdata Guide

## Overview
Masterdata is the necessary base data to run MOSIP services. The data resides in the [`mosip_master` DB](https://github.com/mosip/admin-services/tree/release-1.2.0/db_scripts/mosip_master). This data needs to be customized for a country specific deployment.  Masterdata is bulk uploaded one-time during the [installation process](https://github.com/mosip/mosip-infra/tree/release-1.2.0/deployment/v3/mosip/kernel/masterdata) and later may be updated using the [Admin Portal](admin-portal-guide.md). The default data uploaded during sandbox installation is available in [mosip-data](https://github.com/mosip/mosip-data/tree/release-1.2.0/mosip_master/xlsx).

The tables that would need to be modified are listed below.  Other tables in `mosip_master` DB are either system-filled or pre-filled and not to be modified.

## Common guidelines
* Copy Excel files from [mosip-data](https://github.com/mosip/mosip-data/tree/release-1.2.0/mosip_master/xlsx) to a folder.
* For all tables listed below modify `lang_code` and add corresponding rows for your [configured languages](module-configuration.md#languages). 
* Modify the files for your deployment as per guide below. 
* Upload **first time** using scripts given [here](https://github.com/mosip/mosip-infra/tree/release-1.2.0/deployment/v3/mosip/kernel/masterdata).
* Subsequently, update data ONLY using [Admin Portal](admin-portal-guide.md).

## Tables to be updated
|Category|Table|Guide|
|---|---|---|
|Documents|`doc_category`|Categories of documents to be captured|
||`doc_type`| Specific documents related to a country|
||`applicant_valid_document`|Mapping of document category, type and [applicant type](https://github.com/mosip/mosip-config/blob/develop3-v3/applicanttype.mvel)|
|Location|`loc_hierarchy_list`|List of location hierarchy|
||`location`|List of locations stored in a hierarchical format|
||`loc_holiday`|Holidays specific to different locations. Used in registration centre creation.|
|Machine|`machine_type`|Example mobile, stationary. Refers to `machine_spec`.|
||`machine_spec`|Model, make of the registration machine|
|ID Schema|`identity_schema`| Refer to [ID Schema customisation](id-schema.md). Update the JSON in `schema_json` column of [`identity_schema.xlsx`](https://github.com/mosip/mosip-data/tree/lts/mosip_master/xlsx/identity_schema.xlsx)|
||`dynamic_field`|Dynamic dropdowns used during data capture|
||`id_type`|Only `name` and `descr` can be changed based on language|
||`ui_spec`|UI specification for registration and pre-registration UI screens. See [UI spec guides]()|
|Registration client|`permitted_local_config`|List of changeable configurations by the operator|
||`app_authentication_method`| Only `method_seq` can be changed|
||`app_detail`|Only `name` and `descr` can be changed based on language|
||`app_role_priority`|Only `priority` can be changed|
||`authentication_method`|Only `method_seq` can be changed|
||`reason_list`|List of reasons for a reason category|
||`reason_category`|Only `name` and `descr` can be changed based on language|
|Registration center|`reg_center_type`|Type of center |
||`registration_center`|List of registration centers|
||`registration_center_h`|Historical data for any modification done on a registration center. One time intialization of this table identical to `registration_center`. Thereafter, the data will be system updated|
||`reg_exceptional_holiday`|Exception holiday for a registration center|
||`reg_working_nonworking`|Working and non-working day for a center|
|Biometrics|`biometric_attribute`|Only `name` and `descr` can be changed based on language|
||`biometric_type`|Only `name` and `descr` can be changed based on language|
|Templates|`template`|Only `name`, `descr`, `file_txt` can be changed based on language|
||`template_file_format`|Only `descr` can be changed based on language|
||`template_type`|Only `descr` can be changed based on language|
|Others|`blocklisted_words`|List of blocked words|
||`daysofweek_list`|Only `name` can be changed based on language|
||`module_detail`|Only `name` and `descr` can be changed based on language|
||`process_list`|Only `name` and `descr` can be changed based on language|
||`status_list`|Only `descr` can be changed based on language|
||`status_type`|Only `name` and `descr` can be changed based on language|
||`title`|List of titles used in the country|
||`zone`|List of administrative zones in a country|
