Generic fields (in documents / operations)

- `_attachments`: CouchDB-like attachments; a Map of names to attachment description
- `_deleted`: boolean
- `_id`: string
- `_rev`: string
- `_missing`: boolean (generated e.g. by `ccnq4-opensips`)

CCNQ4-specific generic fields

- `type`: string
- [type]: for any given type, there is a field with the same name that contains the key, such that `_id` == `<type>:<[type]>`
- `disabled`: boolean
- `account`: string
- `sub_account`: string
- `timezone`: string
- `language`: string
- `country`: string

Document-specific
-----------------

### Routing

### type `carrier`

`tough-rate`

- `_id`: `carrier:<sip_domain_name>:<carrierid>`
- `carrier`: `<sip_domain_name>:<carrierid>`
- `carrierid`: string
- `sip_domain_name`: string
- `name`
- `rating`: Map from a start-date (`YYYY-MM-DD`) to a record
- `rating["YYYY-MM-DD"].table`: string, name of the rating table

### type `gateway`

- `address`
- `carrier`
- `carrierid`
- `gwid`
- `sip_domain_name`

also: `disabled`, `name`

### type `emergency`

- `emergency`: `<number>#<emergency-reference>` where number is a called number (e.g. `33_113`) and the reference is the `routing_data` value found in a `location` document.
- `destination`: translated emergency number

### type `location`

- `location`: `<location-reference>`
- `routing_data`: `<emergency-reference>`

### type `destination`

Destinations are defined in `tough-rate` and `entertaining-crib`, but really we're talking about two different object types, so probably need to renamed one of them.

In `tough-rate`: (aka `<routing-destination>`)

- `attrs` (is this obsolete?)
- `emergency`: boolean
- `gwlist`: list
- `gwlist[N].carrierid`: string
- `gwlist[N].gwid`


In `entertaining-crib`: (aka `<rating-destination>`)

- `initial.cost`
- `initial.duration`
- `subsequent.cost`
- `subsequent.duration`

#### type `prefix`

As `<routing-prefix>`

- `attrs`
- `destination`: `<rating-destination>`
- `emergency` boolean
- `gwlist` List
- `gwlist[N].carrierid`
- `gwlist[N].gwid`

As `<rating-prefix>`

- `attrs`
- `destination`: `<rating-destination>`
- `emergency` boolean (?)
- `initial.cost`
- `initial.duration`
- `subsequent.cost`
- `subsequent.duration`

### type `ruleset`

educated-carriage, tough-rate ??

- `key`

### type `device`

Autoprovisioning. (I don't think any of this is public.)

### CDR

`grumpy-actor`

- `actual_amount`

Also, `.variables` in FreeSwitch CDRs

### type `number_domain`

- `number_domain`: `<number_domain>`
- `calendars`: Map or List
- `calendars[NAME]`: List of `YYYY-MM-DD`
- `conferences`: Map or List
- `conferences[NUMBER].record` boolean
- `country`
- `dialplan`: `national`, `centrex`, …
- `fifos`: List
- `fifos[N].default_voicmail_settings`
- `fifos[N].user_database` (defaults to using `fifos[N[.voicemail`)
- `fifos[N].voicemail`
- `fifos[N].announce`: FileName
- `fifos[N].members`: Set
- `fifos[N].members[M].delay`
- `fifos[N].members[M].progress_timeout`
- `fifos[N].members[M].recipient`
- `fifos[N].members[M].timeout`
- `fifos[M].music` FileName
- `fifos[M].progress_timeout`
- `fifos[M].timeout`
- `menus`: Map or List
- `menus[NUMBER]` ???

### type `domain`

These are needed for centrex I believe.

- `admin` (string)
- `domain`
- `expire` (integer)
- `min_ttl`
- `refresh`
- `retry`
- `soa`
- `ttl`
- `records`: Map of names
- `records[NAME].class`
- `records[NAME].ttl`
- `records[NAME].value`

### type `host`

- `host`
- `interfaces`: Map
- `interfaces.internal.ipv4`
- `interfaces.internal.ipv6`
- `interfaces.external.ipv4`
- `interfaces.external.ipv6`
- `opensips.proxy_ip`
- `opensips.proxy_port`
- `sip_domain_name`
- `sip_profiles`: Map
- `sip_profiles[NAME].egress.address`
- `sip_profiles[NAME].egress.carrier`
- `sip_profiles[NAME].egress.carrierid`
- `sip_profiles[NAME].egress.disabled`
- `sip_profiles[NAME].egress.gwid`
- `sip_profiles[NAME].egress_gwid`
- `sip_profiles[NAME].ingress_sip_ip`
- `sip_profiles[NAME].ingress_sip_port`
- `sip_profiles[NAME].egress_sip_ip`
- `sip_profiles[NAME].egress_sip_port`
- `sip_profiles[NAME].egress.host`
- `sip_profiles[NAME].egress.name`

### type `list`

Used for blacklist and whitelist of individual numbers.

- `list`: `<number>@<number_domain>@<caller>`
- `blacklist`: boolean
- `whitelist`: boolean
- `disabled`: boolean

### type `endpoint`

Some fields are related to endpoint-as-destination, others to endpoint-as-source.

#### endpoint as destination

- `dst_disabled`
- `max_channels`
- `password`­— typically never presented
- `rate_limit`
- `sbc` (still active?)
- `user_ip`
- `user_port`
- `user_srv`
- `user_via`

- `rating_interval`
- `rating_ornaments`

#### endpoint as source

- `account`
- `asserted_number`
- `bypass_from_auth`
- `check_from`
- `check_ip`
- `country`
- `dialog_timer`
- `dialplan`
- `inbound_sbc`
- `keep_headers`
- `location`: `<location-reference>`
- `max_channels`
- `number_domain`
- `outbound_domain` dnsDomain
- `password`
- `privacy`
- `rate_limit`
- `rating` Map on `YYYY-MM-DD`
- `rating["YYYY-MM-DD"].plan`
- `rating["YYYY-MM-DD"].table`
- `require_register`
- `require_same_auth`
- `sbc`  (still used?)
- `src_disabled`
- `timezone`
- `user_ip`

### type `number`

Some fields are related to number-as-global-number (no `@` in the number), others to number-as-local-number.

### number as global-number

- `fs_variables`
- `language`
- `local_number`
- `outbound_route` (LCR in tough-rate)
- `timezone`
- `voicemail_number_domain`: string
- `trace`: boolean
- `voicemail_main`: boolean


- `address` (registrant)
- `registrant_host` (registrant)
- `registrant_password`
- `registrant_realm`
- `registrant_remote_ipv4`
- `registrant_socket`
- `registrant_username`

Also: `rating` (injected)

### number as local-number

- `number`: `<local-number>@<number_domain>`
- `asserted_number`
- `country`
- `timezone`

- `custom_music`: FileName (in `voicemail_settings`)
- `custom_ringback`: FileName (in `voicemail_settings`)
- `default_voicemail_settings` (only once)
- `dialog_timer`
- `user_database`
- `voicemail_sender`
- `groups`: Set

Ingress calls only:

- `cfa_enabled`, `cfa_number`, `cfa_voicemail`
- `cfb_enabled`, `cfb_number`, `cfb_voicemail`
- `cfda_enabled`, `cfda_number`, `cfda_voicemail`
- `cfnr_enabled`, `cfnr_number`, `cfnr_voicemail`
- `convergence_active`: boolean
- `convergence`: List
- `convergence[N].number`
- `convergence[N].confirm`: boolean or string
- `convergence[N].delay`
- `convergence[N].timeout`
- `endpoint`
- `endpoint_via`
- `inv_timer`
- `location`: `<location-reference>`
- `ornaments`: List
- `reject_anonymous`
- `reject_anonymous_to_voicemail`
- `ring_ready`
- `use_blacklist`
- `use_whitelist`
- `vacation.end`
- `vacation.start`

Egress calls only:

- `dialplan`: `national` or `centrex`
- `list_to_voicemail` boolean
- `login_commands` (call-center)
- `privacy`: boolean
- `allowed_groups`: Set (call-center)

#### `_id` = `registrant_host_to_server_mapping`

### Rating

#### `_id` = `configuration`

- `currency`
- `divider`
- `per`
- `ready`

####

- `plan`
- `plan.ornaments`

#### `destination` aka `<rating-destination>`
#### `prefix` aka `<rating-prefix>`

### Traces

- type: `trace`
- `packets`: List

### Voicemail (user database)

Views: `new_messages`, `no_messages`, `saved_messages`

#### `_id` = `voicemail_settings`

- `_attachements["name.mp3"]`
- `_attachements["prompt.mp3"]`
- `ask_pin`
- `do_not_record`
- `email_notifications` Map
- `email_notifications[ADDRESS].attach_message`
- `pin`
- `prompt`: `prompt`, `name`, `default`
- `send_then_delete`
- `language`
- `timezone`

Other fields (CouchDB):
- `_revs_info`

Obsolete fields:

- `_in`: needs to be removed
