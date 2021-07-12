# Domains

Here I describe all main domains the project and them properties.

## User

The main object of the whole activities of the TALK44 project.

It has the following properties:

- `id` is unique primary key;
- `email` is as identification  and main channel for OTP and notifications about meetings' events (NB the field has to be encoded);
- `name` and `surname` are real full name for an offline meeting (NB the field has to be encoded);
- `gender_id` is gender ID;
- `is_available` is a flag either the user is available or not;
- `is_removed` is a flag either the user is removed or not;

## Email

To integrate main application with email sender SaaS here is needed to have an extendable table with emails meta-data.

The domain with the properties:

- `user_id` is foreign key and binding to `user` domain;
- `with_notifications` is a flag either the user wants to get notifications about meetings or not.

## OTP (one time password)

This is just one time password that will be sending for login and meeting confirmation.

This domain has:

- `user_id` is foreign key and binding to `user` domain;
- `code` is OTP (NB the field has to be encoded);
- `created_at` is timestamp when the code was created;
- `ttl` is time to live the code.

After using or exceeding the TTL the record has to be removed from information system.

## Session

If a user confirmed own email then the information system creates a session record for client-serve communication.

Session has the following:

- `user_id` is foreign key and binding to `user` domain;
- `token` is session token;
- `created_at` is timestamp when the token was created;
- `ttl` is time to live the token.

After exceeding the TTL the record has to be removed from information system.

## Geo

The domain is as places of living storage to search friends for meetings between the nearest.

Geo contains:

- `id` is unique primary key;
- `lat` is latitude of a geo point;
- `lng` is longitude of a geo point.

## Tag

List of tags is the way to set main topic of a meeting.
For example: #technology #business #internet it implies somebody are looking for friends who can keep up the conversation about IT and business with it.

- `id` is unique primary key;
- `name` is name of a tag.

## Gender

For each of country needs own lists of genders.
A release candidate must work with binary genders only.

- `id` is unique primary key;
- `name` is name of a gender;
- `country_code` is country code.

## Country

The domain is needed to separation genders by countries.

- `code` is unique primary key from [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3);
- `name` is name of a country.

## Meeting

It is one of main domains.
The domain contains all information about meetings.

- `id` is unique primary key;
- `datetime` is date and time of a meeting;
- `duration` is duration of a meeting;
- `is_finished` is flag either a meeting is finished or not.

## Companion

The next of main domains is companion. It is a person who are waiting for planned meeting.

The domain is just binding between `user` and `meeting`.

- `meeting_id` is foreign key and binding to `meeting` domain;
- `user_id` is foreign key and binding to `user` domain.

## POI

It is a place where the initiator would like to hold a meeting.

- `id` is unique primary key;
- `name` is name of POI;
- `lat` is latitude of a geo point;
- `lng` is longitude of a geo point.
- `addr` is POI address;
- `timetable` is a field with POI timetable in JSON format.

## Search engine

It is one of main domains. And this is a search engine for selecting people for a meeting.

It doesn't some properties.

And it has the following filters:

- `geo_id` is foreign key and binding to `geo` domain;
- list of `tag_id` is a list with foreign keys to `tag` domain;
- `gender_id` is foreign key and binding to `gender` domain;
- `initiator_id` is foreign key and binding to `user` domain;
- `poi_id` is foreign key and binding to `poi` domain.