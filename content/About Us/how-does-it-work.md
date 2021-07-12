---
title: "How does this work?"
date: 2021-07-08T16:12:33-04:00
draft: false
---

## The Scripts

The entire process starts with a script that collects the data in its current, less-than-usable, format and convertings the data into JSON.  These scripts are stored in our [GitHub repository](https://github.com/DataForNerds/public) under the scripts folder. When the script runs, it outputs the data into the content folder within the repository.

## The GitHub Actions

We're fortunate the GitHub has provided an easy way to run PowerShell scripts on a scheduled basis using PowerShell Core running on Ubuntu. These jobs are triggered on a regular schedule and are stored in the [.github/workflows](https://github.com/DataForNerds/public/tree/main/.github/workflows) folder of the repository.  When there is an update to the file, the action automatically generates a pull request for the change and a DataForNerds contributer verifies that it's OK and then accepts the pull request, which updates the main repository.

## The Content Delivery Network

As GitHub as limits to how often you can hit a repository before they start asking the owner to host somewhere else, we're using Amazon's CDN in front of the GitHub repository.  The CDN, named [CloudFront](https://aws.amazon.com/cloudfront/features/), caches our content across hundreds of servers across the globe for quick and easy access to the data.  We typically cache pages for about an hour.  We do ask that even when you inevitably find out what the underlying URLs are for the content behind the CDN that you continue to use the CDN address as it's there to take the load off of the backend, ensure we comply with our hosts wishes, and also should never change even as the background infrastructure does change.