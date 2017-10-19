---
title: 'Creating Software Release from CD Pipeline - VIPER'
viewport: |
    width=device-width, initial-scale=1.0, minimum-scale=1.0,
    maximum-scale=2.0, user-scalable=yes
---

<div id="ht-loader">

</div>

<div>

<div class="ht-headerbar-left">

[](){#ht-menu-toggle .sp-aui-icon-small .sp-aui-iconfont-appswitcher}

</div>

<div class="ht-headerbar-right">

<div class="sp-aui-icon-small ht-search-index-loader ht-header-icon">

</div>

<div id="ht-search">

<div class="ht-search-input" style="display: none;">

[](#){.sp-aui-icon-small .sp-aui-iconfont-remove .ht-search-clear}
<div class="ht-search-dropdown ht-dropdown">

</div>

</div>

</div>

</div>

<div class="ht-sidebar-content">

<div class="ht-sidebar-content-scroll-container">

[VIP]{.ht-logo-label} ![](spacelogo.png){.space-logo} {#vip .ht-logo}
=====================================================

[](Creating_Software_Release_from_CD_Pipeline.html){.ht-space-link}
VIPER
-----

-   [Creating Manual Software Release from CD
    Pipeline](Creating_Manual_Software_Release_from_CD_Pipeline.html){.ht-nav-page-link}

</div>

</div>

</div>

<div id="ht-wrap-container">

<div id="ht-sidebar-dragbar">

<div class="ht-sidebar-drag-handle">

[]{.drag-handle-1} []{.drag-handle-2} []{.drag-handle-3}

</div>

</div>

<div id="ht-breadcrumb">

-   [VIPER](Creating_Software_Release_from_CD_Pipeline.html)

</div>

[Creating Software Release from CD Pipeline]{} {#src-124815252}
==============================================

<div id="main-content" class="wiki-content sp-grid-section"
data-index-for-search="true">

<div id="src-124815252_CreatingSoftwareReleasefromCDPipeline-Overview"
class="section section-1">

[Overview]{} {#overview .heading}
============

This guide describes the process to create a release from the CD
Pipeline.

The CD Pipeline creates a bi-daily build at 2 AM and 2 PM MST. A manual
build can be triggered at any time.

All builds are tagged in the rio-workspace repo with the timestamp
serving as the tag name.

Information about the generated build can be found in the \#rio-cd slack
channel.

The pipeline can be found here:
<https://concourse.ee.viperx.org/teams/rio/pipelines/cd-dev-next>

</div>

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-Beforestarting"
class="section section-1">

[Before starting]{} {#before-starting .heading}
===================

Make any required Geronimo configuration changes. Be sure to check with
the team as there may be late breaking changes that may not have been
communicated. Normally these changes would have been done as part of the
associated feature or bugfix change.

The config files are located in `.../rio-workspace/kube/rio.`

<div class="confbox programlisting">

<div class="defaultnew syntaxhighlighter scroll-html-formatted-code"
xmlns="http://www.w3.org/1999/xhtml">

<div class="line">

`There may be site specific overrides needed to any new or existing environment variables found in base.json.`{.plain}

</div>

<div class="line">

` `{.plain}

</div>

<div class="line">

`The override files for each environment can be found in rio/environments/site_specific/<env>.json. <env> is one of <detroit, albq, tc> for prod environments, and <qa-next, dev-next, qa-perf, qa-long, dev-qa-master> for lab environments.`{.plain}

</div>

<div class="line">

` `{.plain}

</div>

<div class="line">

`Also, the base file is overridden by the specific files in this order:`{.plain}

</div>

<div class="line">

`     * Prod - base.json, prod_zookeeper.json followed by site_specific/<env>.json`{.plain}

</div>

<div class="line">

`     * Labs - base.json, labs.json followed by site_specific/<env>.json`{.plain}

</div>

</div>

</div>

If you had to make any Geronimo configuration changes have another team
member review the changes before proceeding with the next steps below.
This can be done by having them review the commit in Github.

The SATs that are run are found in rio-workspace/sats. To change the SAT
versions, modify the files there.

<div class="confbox programlisting">

<div class="defaultnew syntaxhighlighter scroll-html-formatted-code"
xmlns="http://www.w3.org/1999/xhtml">

<div class="line">

`[vagrant`{.plain}`@rio`{.color1}`-dev sats]$ ls -al`{.plain}

</div>

<div class="line">

`total `{.plain}`28`{.value}

</div>

<div class="line">

`drwxrwxr-x `{.plain}`2`{.value}` vagrant  `{.plain}`139`{.value}` Feb `{.plain}`20`{.value}` `{.plain}`19`{.value}`:`{.plain}`43`{.value}` ./`{.plain}

</div>

<div class="line">

`drwxrwxr-x `{.plain}`8`{.value}` vagrant `{.plain}`4096`{.value}` Feb `{.plain}`13`{.value}` `{.plain}`16`{.value}`:`{.plain}`40`{.value}` ../`{.plain}

</div>

<div class="line">

`-rw-rw-r-- `{.plain}`1`{.value}` vagrant  `{.plain}`782`{.value}` Jan  `{.plain}`5`{.value}` `{.plain}`17`{.value}`:`{.plain}`38`{.value}` sat-pod-a8.json`{.plain}

</div>

<div class="line">

`-rw-rw-r-- `{.plain}`1`{.value}` vagrant  `{.plain}`748`{.value}` Jan  `{.plain}`5`{.value}` `{.plain}`17`{.value}`:`{.plain}`38`{.value}` sat-pod-aa.json`{.plain}

</div>

<div class="line">

`-rw-rw-r-- `{.plain}`1`{.value}` vagrant  `{.plain}`759`{.value}` Feb `{.plain}`20`{.value}` `{.plain}`19`{.value}`:`{.plain}`43`{.value}` sat-pod-`{.plain}`do`{.keyword}`.json`{.plain}

</div>

<div class="line">

`-rw-rw-r-- `{.plain}`1`{.value}` vagrant  `{.plain}`782`{.value}` Jan  `{.plain}`5`{.value}` `{.plain}`17`{.value}`:`{.plain}`38`{.value}` sat-pod-lp.json`{.plain}

</div>

<div class="line">

`-rw-rw-r-- `{.plain}`1`{.value}` vagrant  `{.plain}`457`{.value}` Jan  `{.plain}`5`{.value}` `{.plain}`17`{.value}`:`{.plain}`38`{.value}` sat-pod-n8.json`{.plain}

</div>

<div class="line">

`-rw-rw-r-- `{.plain}`1`{.value}` vagrant  `{.plain}`277`{.value}` Jan  `{.plain}`5`{.value}` `{.plain}`17`{.value}`:`{.plain}`38`{.value}` sat-service.json`{.plain}

</div>

</div>

</div>

</div>

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-SelectingARelease"
class="section section-1">

[Selecting A Release]{} {#selecting-a-release .heading}
=======================

To select the release start by clicking on one of the builds
(deploy-morning, deploy-afternoon, deploy-manual-newest,
deploy-manual-canticle).

-   *deploy-morning* - pipeline for the 2 AM daily build

-   *deploy-afternoon* - pipeline for the 2 PM daily build

-   *deploy-manual-newest* - pipeline that will create a new build based
    on the latest version for all components (see [Kick Off A Manual CD
    Build](#src-124815252_CreatingSoftwareReleasefromCDPipeline-KickOffAManualCdBuild)
    below)

-   *deploy-manual-canticle* - pipeline that will create a new build
    based on the Canticle file found in rio-workspace. Please use the
    guide [here](Creating_Manual_Software_Release_from_CD_Pipeline.html)
    to create a manual build from the Canticle file.

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_10_01_45_AM.png){.confluence-embedded-image
height="250"}

For each build, the CD pipeline will indicate a successful build with a
green background. The builds with the green background are candidates
for the release.

<div class="tablewrap">

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_10.14.45_AM.png){.confluence-embedded-image}

Successful Build

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_10.16.15_AM.png){.confluence-embedded-image}

Unsuccessful Build

</div>

</div>

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-KickOffAManualCdBuildKickoffamanualCDbuild"
class="section section-1">

[Kick off a manual CD build]{} {#kick-off-a-manual-cd-build .heading}
==============================

[ Click on the **deploy-manual-newest** pipeline and then click on the
plus button on the top right. ]{style="color: #000000;"}

[
![](images/download/attachments/124815252/Screen_Shot_2017-01-23_at_9.42.17_AM.png){.confluence-embedded-image
height="250"}\
]{style="color: #000000;"}

</div>

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-GetTheBuildTagGettheBuildTag"
class="section section-1">

[]{#src-124815252_CreatingSoftwareReleasefromCDPipeline-GetTheBuildTag .confluence-anchor-link}[Get the Build Tag]{} {#get-the-build-tag .heading}
====================================================================================================================

Once a build has been selected, the build tag must be retrieved. The
build tag can be found at the bottom of the **update-geronimo** step in
concourse. To expand the logs of the **update-geronimo** step, simply
click on it. You should see a line like
`* [new tag]         2017.01.23-20.29.18 -> 2017.01.23-20.29.18` in the
pipeline's output. Remember this build tag as it is used in the
[Finalizing
Release](#src-124815252_CreatingSoftwareReleasefromCDPipeline-FinalizingRelease)
step below.

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_10_19_57_AM.png){.confluence-embedded-image
height="250"}
![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_10_20_09_AM.png){.confluence-embedded-image
height="250"}

So for this example release, the tag ***2016.12.31-21.01.42*** is
chosen.

</div>

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-RetrievingReleaseNotes"
class="section section-1">

[Retrieving Release Notes]{} {#retrieving-release-notes .heading}
============================

Next, the release notes must be copied and sent out. The release notes
can be found under the **propose-release** step in concourse.

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_10_27_41_AM.png){.confluence-embedded-image
height="250"}

The *short format* is used to update the [Rio release
notes](https://www.teamccp.com/confluence/display/VIP/RIO+Release+Notes){.external-link}
and the *long format* is used for the email that is sent for
verification (send to rio-dev-ext@comcast.com).

[ **NOTE** ]{style="color: #ff0000;"} : The release notes should also
include details regarding major changes such as new environment
variables, new or updated SATs, and database schema changes. Schema
changes should be described in detail at [Rio Database
Migrations](https://etwiki.sys.comcast.net/display/VIP/Rio+Database+Migrations).
Verify this before creating the release notes.

For each build, the CD pipeline will generate the release notes that are
based on the last production release created. Release notes matching the
following regex: \[1-9\].\[0-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].

</div>

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-FinalizingReleaseFinalizingRelease"
class="section section-1">

[]{#src-124815252_CreatingSoftwareReleasefromCDPipeline-FinalizingRelease .confluence-anchor-link}[Finalizing Release]{} {#finalizing-release .heading}
========================================================================================================================

Once all parties have agreed on the release, it must be finalized. This
process tags a pipeline build (with timestamp tag format) with a RIO
version (that matches the following regex:
rio-\[1-9\].\[0-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\]) and updates the
Geronimo system files appropriately.

To do this, go to rio-workspace repo and checkout the production-release
branch and make sure all the local branch is in sync with the remote
branch.

<div class="confbox programlisting">

<div class="defaultnew syntaxhighlighter scroll-html-formatted-code"
xmlns="http://www.w3.org/1999/xhtml">

<div class="line">

`cd rio-workspace`{.plain}

</div>

<div class="line">

`git checkout production-release`{.plain}

</div>

<div class="line">

`git fetch --tags`{.plain}

</div>

<div class="line">

`git pull --rebase origin production-release`{.plain}

</div>

</div>

</div>

Once this is complete modify the
**[version.manifest](https://github.com/rio-cdvr/rio-workspace/blob/production-release/version.manifest){.external-link}**
file found in the root of rio-workspace. Update the `Commit` line with
the build number we got from the [Get The Build
Tag](#src-124815252_CreatingSoftwareReleasefromCDPipeline-GetTheBuildTag)
step above, and update the `Tag` line with the newly desired RIO release
version name (usually Jiang will tell us what to use).

<div class="confbox programlisting">

<div class="defaultnew syntaxhighlighter scroll-html-formatted-code"
xmlns="http://www.w3.org/1999/xhtml">

<div class="line">

`#Sample version.manifest file`{.plain}

</div>

<div class="line">

`{`{.plain}

</div>

<div class="line">

`  `{.plain}`"Commit"`{.string}`:`{.plain}`"2016.12.31-21.01.42"`{.string}`, #CD build tag to use `{.plain}`for`{.keyword}` the `{.plain}`new`{.keyword}` RIO release`{.plain}

</div>

<div class="line">

`  `{.plain}`"Tag"`{.string}`:`{.plain}`"rio-1.1.0-001"`{.string}` #Desired RIO release version`{.plain}

</div>

<div class="line">

`}`{.plain}

</div>

</div>

</div>

This example version.manifest file will use the CD build
**2016.12.31-21.01.42** to create RIO version **rio-1.1.0-001**.

Once the version.manifest file has been changed, it must be committed to
remote.

<div class="confbox programlisting">

<div class="defaultnew syntaxhighlighter scroll-html-formatted-code"
xmlns="http://www.w3.org/1999/xhtml">

<div class="line">

`git add version.manifest`{.plain}

</div>

<div class="line">

`git commit -m `{.plain}`"Creating release version rio-1.1.0-001"`{.string}

</div>

<div class="line">

`git push origin production-release`{.plain}

</div>

</div>

</div>

After the commit has been made to the remote (origin), go to
**commit-release** builds in concourse. This final step will use the
version.manifest file from above to build the release with all the right
tags.

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_11_27_28_AM.png){.confluence-embedded-image
height="250"}

Once in the **commit-release** build, click the + button in the top
right corner.

![](images/download/attachments/124815252/Screen_Shot_2017-01-03_at_11_26_28_AM.png){.confluence-embedded-image
height="250"}

If the new build is successful, it will be marked green and a
confirmation message is sent to the \#rio-cd slack channel. The release
has been finalized and committed to the remote!

<div
id="src-124815252_CreatingSoftwareReleasefromCDPipeline-PushReleaseImagestodockerhub"
class="section section-2">

[Push Release Images to dockerhub]{} {#push-release-images-to-dockerhub .heading}
------------------------------------

After a release is created, follow the instructions below to push images
to dockerhub manually.

<div class="confbox programlisting">

<div class="defaultnew syntaxhighlighter scroll-html-formatted-code"
xmlns="http://www.w3.org/1999/xhtml">

<div class="line">

`This procedure is only valid until we have Jenkins or the CD pipeline automatically push to dockerhub.`{.plain}

</div>

<div class="line">

 

</div>

<div class="line">

`# SSH into jenkins machine`{.plain}

</div>

<div class="line">

`$ ssh root`{.plain}`@10`{.color1}`.252.`{.plain}`197.137`{.value}

</div>

<div class="line">

 

</div>

<div class="line">

`# login`{.plain}

</div>

<div class="line">

`# change user as Jenkins`{.plain}

</div>

<div class="line">

`$ su jenkins`{.plain}

</div>

<div class="line">

 

</div>

<div class="line">

 

</div>

<div class="line">

`# Change directory to rio-workspace and checkout the Rio version you want to push`{.plain}

</div>

<div class="line">

`$ cd ~/rio-workspace`{.plain}

</div>

<div class="line">

`$ git fetch`{.plain}

</div>

<div class="line">

`$ git checkout <your version. ex: rio-`{.plain}`1.2`{.value}`.`{.plain}`0`{.value}`-`{.plain}`003`{.value}`>`{.plain}

</div>

<div class="line">

 

</div>

<div class="line">

 

</div>

<div class="line">

`# Run `{.plain}`this`{.keyword}` command to find the specific tags `{.plain}`for`{.keyword}` various components based on the Rio system version and retag those images and push them to dockerhub`{.plain}

</div>

<div class="line">

`$ `{.plain}`for`{.keyword}` img in $(cat kube/rio/systems/rio.json | jq -r `{.plain}`'.spec.components[] | .imagePath + ":" + .tag'`{.string}`|grep -v redis); `{.plain}`do`{.keyword}` oldimg=registry.vipertv.net/$img; newimg=$(echo $img | sed `{.plain}`'s/rio/riocdvr/'`{.string}`); echo `{.plain}`"$oldimg => $newimg"`{.string}`; docker tag `{.plain}`"$oldimg"`{.string}` `{.plain}`"$newimg"`{.string}` && docker push `{.plain}`"$newimg"`{.string}`; done`{.plain}

</div>

<div class="line">

 

</div>

<div class="line">

`# As `{.plain}`this`{.keyword}` command runs, verify the logs from it and see `{.plain}`if`{.keyword}` the image it pushed shows up on dockerhub. If you something amiss, kill the process and save the logs `{.plain}`for`{.keyword}` analysis`{.plain}

</div>

<div class="line">

 

</div>

<div class="line">

`# The path to the repos in dockerhub is https:`{.plain}`//hub.docker.com/u/riocdvr/dashboard/`{.comments}

</div>

<div class="line">

`# Click on the project and then click on the Tags section to see your `{.plain}`new`{.keyword}` tag being created.`{.plain}

</div>

</div>

</div>

</div>

</div>

</div>

[Creating Manual Software Release from CD Pipeline]{}
<div id="ht-spacetitle">

-   [VIPER](Creating_Software_Release_from_CD_Pipeline.html)

</div>

Search results
==============

<div id="search-results">

</div>

[](#){#ht-jump-top .sp-aui-icon-small .sp-aui-iconfont-arrows-up}

</div>

<div>

<div id="ht-mq-detect">

</div>

</div>
