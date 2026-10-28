# User Stories

## BWL1: Information before installation

As BWL lecturer, I want to see detailed information and requirements of an app or VM before installation so that I can judge whether it is suitable for my course.

*Acceptance criterias:*
- [ ] Lecturer can view an app details page from the catalog before initiating any deployment.
- [ ] The app details page displays a description, software stack, VM topology, and minimum hardware requirements.
- [ ] Version information, author, release date, and release notes are displayed.

## BWL2: Start preconfigured environment with few clicks

As BWL lecturer, I want to start a preconfigured learning environment with just a few clicks so that I can begin teaching immediately without configuration overhead.

*Acceptance criterias:*
- [ ] Each app card in the catalog offers a visible "Quick Deploy" action.
- [ ] Clicking Quick Deploy opens a dialog to select the target course or "Only for me".
- [ ] All variables and settings are automatically populated with defaults, skipping the configuration wizard directly to the review step.
- [ ] Falls back to the full wizard if an app requires mandatory inputs without default values.

## BWL3: Recommendations and assistance for configuration

As BWL lecturer, I want recommendations and help for configurations so that I can choose the right settings for my use case without deep technical knowledge (e.g. tooltips, prefilled defaults, 'Recommended' badges).

*Acceptance criterias:*
- [ ] Input fields with author defaults are prefilled on load.
- [ ] Recommended choices in dropdowns (e.g. flavors, networks) are marked with a "Recommended" badge and sorted to the top.
- [ ] Optional settings with working defaults are collapsed by default behind an "Advanced settings" section.
