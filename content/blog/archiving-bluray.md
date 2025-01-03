+++
date = '2024-02-25T12:02:00Z'
lastmod = '2024-02-25T12:02:00Z'
draft = false
title = 'Archiving on Optical Media'
description = 'Keeping BluRay relevant.'
tags = ['tech']
+++

## Preface

Always backup your data.

Many times throughout my life, I found myself realising that I've lost files that I either deem important or realised that I wanted to revisit them only after deletion or tidying up my storage. This leads to annoying cycles of having to rebuild multimedia collections or discovering that something I wish to reobtain has become lost media; Not a pleasant feeling, even for mundane and unimportant files.

While trying to figure out ways to organise my life in various ways as part of a new year's resolution, I've decided that I never want to find myself in this situation again.

## Pre-Existing Setup

Rather than relying on my PC's internal storage, I've been using a Synology DS920+ NAS for many years now. Any large files such as my media collection, or anything that's not immediately required locally is kept on the NAS.

The system is configured with four 4TB Seagate IronWolf hard drives in a Synology Hybrid RAID (SHR) array. This setup provides a total usable storage capacity of 11TB, while also allowing for redundancy with 1 drive failure tolerance.

As RAID is not a form of backup, the NAS is configured to automatically back up to an AWS S3 bucket periodically, with limited version history, via Synology Hyper Backup.

## Backup and Archive

While very effective day to day, I wanted to expand this setup to also include true data archival alongside my existing approach to backup. Even with limited version control on my S3 bucket, it's possible for files to eventually be lost. Additionally, relying solely on one cloud-based storage service with a recurring monthly cost didn't feel like a completely sound solution.

I wanted to fully embrace the 3-2-1 approach to backup -- 3 copies of data on 2 different types of media with 1 off-site.

When considering possible options, Blu-ray discs may not be the first thing to come to mind. Optical media feels like a relic of the 2000s, with a higher price per GB than hard drives and significantly lower capacity per disc than today's flash drives or SD cards.

Despite this, Blu-ray has several key advantages.

Optical Media is a WORM (Write Once Read Many) format. Data burnt to a disc can't be removed or modified. RW discs are an exception, but this is outside the scope of this article and scenario. Once archival data has been burnt to a disc, it can only be retrieved without the possibility of being mistakenly overwritten, modified or deleted in order to free up space for other files (only to be regretted later). This could also act as a layer of security, preserving data integrity and guaranteeing that it wasn't been tampered with, especially in a business setting.

Another major advantage of optical media for long-term archival is the durability of the medium and immunity to bit rot or other forms of degradation. It's commonly accepted that flash storage such as SSDs can only reliably store data for 1-2 years. This duration might be slightly higher for hard drives, but they're more susceptible to bit rot and physical wear of their moving components. This makes both formats suboptimal for long-term cold storage. When stored properly, Blu-rays, even standard non-archival-grade discs, will reliably retain data for decades.

Datacentres will typically rely on LTO tape for backup as they offer much higher capacity per tape than even the largest 100GB BDXL discs and a better price per GB, but the upfront cost of LTO drives and their inherent impracticality makes Blu-ray the home user/hobbyist's go-to alternative.

## My Current Setup

I use a Hitachi-LG BH16 internal BD drive. Practically all Blu-ray drives are identical, but it's useful to confirm compatibility with higher capacity formats such as BDXL and archival M-Disc.

Currently, I use standard 25GB Verbatim BD-R discs, which I plan to archive all of my personal files, photos, videos on music library to. M-Disc may be a consideration in the near future, especially for my most important data, but I wanted to first test out my (still work in progress) system and ensure that it will meet my needs before investing in more expensive discs.

Data due to be burnt to BD has been organised by category into ≈22GB batches which have then been burnt to BDs at a low speed.

Each disc is labelled with a code & date. It is then catalogued in [Virtual Volumes View](https://www.fsoft.it/VVV/). This software stores the filenames and matadata of the discs' content in a local database, which allows quickly looking up the specific disc a given file is archived on for easy retrieval.

This approach is still a work in progress which may change over time. I am yet to find a good solution for keeping track of which files on my NAS are due to be archived in a given folder structure; Currently it's a case of cross-referencing dates of file creation/modification against my VVV catalog.

Please expect some further writing from me on this topic as I refine my workflow.
## Credits

Special thanks to the [Data Hoarder](https://www.reddit.com/r/DataHoarder/) subreddit for getting my interested in the subject matter and to [Daniel Rosehill](https://www.youtube.com/@danielontech) for inspiring the use of Blu-ray and my current workflow.