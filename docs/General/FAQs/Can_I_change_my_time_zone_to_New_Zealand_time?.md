---
created_at: '2018-09-20T23:52:07Z'
hidden: false
label_names: []
position: 0
title: Can I change my time zone to New Zealand time?
vote_count: 6
vote_sum: -4
zendesk_article_id: 360000473256
zendesk_section_id: 360000039036
---

The time displayed in your shell is controlled by a system variable
called `TZ`. To change to New Zealand time you need to set the variable
as follows:

    export TZ="NZ"

This setting will automatically adjust for daylight saving, since the
`tzdata` package is installed at the system level. Our system engineers
will keep the `tzdata` package up to date.

## Making the change persistent

You can make your time zone setting persistent by adding the above line
to your `~/.bashrc`. If you do this, we recommend adding the following
line to your `~/.bash_profile`, or to your `~/.profile` if you have the
latter but not the former:

    test -r ~/.bashrc && . ~/.bashrc

Please see the article, "[.bashrc or
.bash\_profile?](https://support.nesi.org.nz/hc/en-gb/articles/360001194536)"
for more information.

## What about cron jobs?

To have the specifications in your crontab file interpreted as NZ times
start it with:

    CRON_TZ=NZ

Also note that cron does not source either `~/.bashrc` or
`~/.bash_profile`, so most environment variables will not be set,
including TZ.
