# GitHub Action Runner Reference


Until someone other than my mom thinks this is neat, this will likely just be collection markdown files, images, and Action logs as favor
to future me. 

## Wut

Just a quick, high level reference guide with information about how GitHub Action Runners are configured by default.

Examples:
* Environment Variables across different os versions
* Location of different executables across os versions
* Default configuration values for common applications (git, python, etc) across os versions
* Values for different System Profile information across os versions (processor speed, num processors, num cores, etc)
* List of processes that are running by default
* The shape or key/values of various [GitHub Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
* Contents/checksum of well known/common files


### You can browse the `GITHUB_ACTIONS_SUMMARIES` for each OS in the [**Actions** Tab](https://github.com/deric4/nsfw-ghar-mess-around/actions/runs/3230724804)

<p align="center">
  <a href="https://github.com/deric4/nsfw-ghar-mess-around/actions/runs/3230724804">
  <img src="https://github.com/deric4/blobs/blob/main/gif-ghar-mess-around.gif"/>
  </a>
</p>

## Why

Over the years I've helped **DevSecOpsLeanSREAgileBBQWTF** teams, from small startups to Fortune 100 enterprises design, develop, maintain thousands of CICD pipelines for both Application and Infrastructure-as-Code code bases.

Regardless of whether your CICD pipeline has a single stage/step/job in a greenfield environment or it's a complex rats nest responsible for a business critical application, there are a few patterns/methods/ideas/industry common practices (I hate the term _best practice_ ) I've compiled into a personal framework of sorts that helps decrease the risk of introducing changes which may cause downstream jobs fail, artifacts to be built with incorrect dependencies, or other silent errors that slip into production.

Understanding the execution environment of each job can dramatically reduce the amount of time it takes to debug errors. Unfortunately, gathering this metadata while debugging individual pipeline steps is usually an iterative process and the feedback loop for making a change as simple as a typo is usually in the order of minutes.

There are numerous ways to keep track of your execution environment(s) and there a plenty of blogs/resources out there, but the most effective,reliable, and "production" worthy has been to create base images (for both virtual machines and docker/OCI images) and to layer/build on top of well-known/common images to create your own "golden images" tailored to your requirements.

> Google search ‘golden image ami’ or ‘golden docker image’

> A good overview might be the [HashiCorp Cloud Platform documentation on building your own custom golden image pipeline](https://learn.hashicorp.com/tutorials/packer/golden-image-with-hcp-packer?in=packer/cloud-production)

The Runners used by GitHub Actions take this approach and include a variety of default tools and configuration intended to make it easier to get started with GitHub actions but can pollute/change the executions runtime environment in unexpected/unpredictable ways and adds a not so insignificant amount of cognitive overhead when debugging (most likely an acceptable compromise for smaller/opensource projects, considering the alternative of hosting your own runner). For better or worse, most workflows leverage the use of “actions” to bootstrap the runtime environment for your jobs.


These actions behave differently depending on the specified os version, configuration options, or any permutation of the two and it's not uncommon for these actions to manipulate the `$PATH` environment variable which can have unintended consequences in subsequent commands/actions.

The hope is that this reference guide can dive just a _little bit_ deeper than what's currently documented by GitHub and save developers a few minutes or more when troubleshooting some high level issues and make it easier to spot differences between a “relatively clean” runtime environment and the environment you as the developer are debugging.

You can see how the GHA Runner Images are created and what additional tooling and version is installed in the [actions/runner-images repo](https://github.com/actions/runner-images) (strongly recommend glancing through the markdown files at least once).

## Contributing

If you have an suggestion on what would make this reference more useful for you, please don't hesitate to open an Issue or Discussion along with any specific commands (with nice markdown formatting plz).

Since future me is most likely to benefit the most from this project (or even see it :upside_down_face:) I'll wait till theres at least one other contributor to setup an issue/template
