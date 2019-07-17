## Adding the Agency Tag to Campaign Name

Only agencies managing advertising campaigns on behalf of a client must prepend their `Agency ID` to the campaign name when creating advertising campaigns for Self-Attributing Networks (SANs).  

!!! error "Agency ID Required"
	Failure to append the campaign name with the `Agency ID` will result in any subsequent conversion not being properly attributed to the responsible agency.

### Finding Your Agency ID

You can find your Agency ID under Account Settings in the [Agency view](/dashboard/agency-view/#managing-your-agency-profile).

### Creating Your Agency Tag

Your agency tag **must** adhere to the following format:

	`agency_{YOUR AGENCY ID HERE}_`


!!! info "Example Campaign with Agency tag"
 	`agency_1234567890_My_SAN_Ad_Campaign`

	You can append the Agency Tag to either the **beginning** or the **end** of the campaign name.

!!! warning "Agency ID Removed When Exporting"
	The "~campaign" value displayed in exports/analytics will not include the agency_id. If you set up a campaign called `test_campaign_agency_1234` in Facebook, and for any installs that came from that campaign, the "~campaign" value will be "test campaign".
