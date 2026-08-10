# How Patch My PC Cloud Update Rings Affect Dependencies

_Applies to: Patch My PC Cloud_

If your deployments are using [App Dependencies](../deploy-app/configurations-tab/additional-tools/dependencies.md) and both the deployments for the child and parent apps have Update Rings enabled, the following behavior occurs:

* Each version of an app for the child deployment with update rings enabled must depend on the parent app with the version related to the last ring of the parent deployment.
* When the last ring of the parent app is updated to a new version, we also move over the dependencies associated with the last ring.
* If Update Rings are disabled for the parent app, we rebuild the dependency with the app that used to be Ring 1, with the lowest delay/the latest version.
* If the delay for the ring with the oldest version is decreased and this ring becomes the ring with the newest version, we will delete the previous dependency and build the dependency with the app that, after editing, has the oldest version.
