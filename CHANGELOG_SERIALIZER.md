# Serializer changes

## v2

### Release 1.4.2

* AccountSerializer.branch_codes cannot be empty any more
* OrderLineGoogleAdsBasicSerializer.regions cannot be empty any more
* OrderLineSeoSerializer.topics cannot be empty any more
* OrderLineSeoSerializer.regions cannot be empty any more

### Release 1.4.1

#### `OrderLineLandingpageSerializer`
added, similar to `OrderLineWebsiteSerializer` except for
* `additional_subpages`: positive integer, required
* `logo_creation`: choice of `LOGO_CREATION_CHOICES`, required

#### `OrderLineSerializer`
* added `detail_landingpage`: type `OrderLineLandingpageSerializer`, only required when OrderLine represents a landingpage product

#### `OrderLineGoogleAdsBasicSerializer`
* added `target_page_type`: choice of `GOOGLE_ADS_LANDING_PAGE_CHOICES`, optional
    * see `Serializer` changes for validation

#### `OrderLineGoogleAdsPremiumSerializer`
* added `branch_codes`: list of HeroCentral provided industry topic codes, optional
    * HeroCentral will validate the codes against the industry tree
* added `target_page_type`: choice of `GOOGLE_ADS_LANDING_PAGE_CHOICES`, optional
    * see `Serializer` changes for validation
* added `remarketing_setup_fee`: decimal, must be >=0 if `include_remarketing=true`
* added `remarketing_budget`: decimal, must be >=0 if `include_remarketing=true` 

#### Serializer
* added validation: if any OrderLine detail contains `target_page_type`
    * if set to `NEW_WEBSITE`, the serializer will require an OrderLine of type `PRODUCT_TYPE_WEBSITE` to exist
    * if set to `NEW_LANDINGPAGE`, the serializer will require an OrderLine of type `PRODUCT_TYPE_LANDINGPAGE` to exist
    * OrderLine details which can provide values for `target_page_type` are: 
        * OrderLineDisplayBasicSerializer
        * OrderLineDisplayPremiumSerializer
        * OrderLineSeoSerializer
        * OrderLineInAppSerializer 
        * OrderLineFacebookSerializer
