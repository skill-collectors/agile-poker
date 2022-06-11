# Contributing to agile-poker

Welcome to the agile-poker development community! We're glad you're here. This
document is designed to help you get your bearings and then to find something
fun to work on.

Have questions, or just want to say "Hi"? [Join the chat on
gitter.im](https://gitter.im/skill-collectors/agile-poker)!

## Getting started

Clone the project

```bash
git clone https://github.com/dave-burke/agile-poker.git
```

Go to the project directory

```bash
cd agile-poker
```

Run the bootstrap script

```bash
./bootstrap.sh
```

This script should work on Linux and MacOS. A Windows script would need to be
written.

The bootstrap script is meant to be repeatable; if you run it a second time it
should not hurt anything. That means if we add something to it later, people
who already ran it before can just run it again to gain the additional setup.

## Recommended IDE Setup

The recommended IDE is [VSCode](https://code.visualstudio.com/). Select `File
-> Open Workspace from File...` and choose `.vscode/project.code-workspace`.

VSCode will offer to install the following recommended extensions:

- [Svelte](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode)
- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

Workspace settings should be configured to lint and format-on-save correctly.

## Running the code

### Frontend

The web interface uses the [Svelte](https://svelte.dev/) framework with
[SveltKit](https://kit.svelte.dev/). If these are new to you, we recommend you
try the [Svelte tutorial](https://svelte.dev/tutorial/basics) and review the
[SvelteKit documentation](https://kit.svelte.dev/docs/introduction).

To start the frontend server:

```bash
cd frontend
npm run dev
```

Browse to http://localhost:3000

#### Tests

The frontend uses [Vitest](https://vitest.dev/) for unit testing and
[Playwright](https://playwright.dev/) for end-to-end (e2e) testing.

Unit test coverage should be as close to 100% as is reasonable. You can check
code coverage by running `npm run coverage`.

E2E tests should cover basic scenarios mostly for sanity checking after a
deploy.

#### Styles

This project uses [Windi CSS](https://windicss.org/) for styling. Windi CSS is
a [utility-first](https://utilitycss.com/) CSS framework. It is compatible with
[Tailwinds](https://tailwindcss.com/) which means you can use [this
cheatsheet](https://tailwindcomponents.com/cheatsheet/).

Basically, instead of this:

```html
<button class="myButton">Click me!</button>
<style>
.myButton {
	background-color: #047857; /* Green */
	border: none;
	color: white;
	padding: 1rem;
	text-align: center;
}
</style>
```

You do this:

```html
<button class="bg-green-700 border-none text-white p-4 text-center">
	Click me!
</button>
```

Why would you do this? [Read
this](https://adamwathan.me/css-utility-classes-and-separation-of-concerns/)
for more context. The short answer is that it works well with scoped CSS in
component frameworks like Svelte.

### Infrastructure

This project uses [Pulumi](https://www.pulumi.com/) to create the necessary AWS
resources for the project. That includes S3/Cloudfront for the frontend and
Labmda/API Gateway/DynamoDB for the backend.

#### Local development

This project uses [LocalStack](https://localstack.cloud) to mock cloud services
locally using [Docker](https://docs.docker.com/).  This enables you to "deploy"
the infrastructure and run it locally to test without needing an AWS account or
even an internet connection!

If you ran `bootstrap.sh` successfully, then you should now have `localstack`
installed. Run the following commands to bring up the project infrastructure on
your localstack:

```
localstack start -d
pulumi stack select dev
pulumi up
```

#### Unit testing

Like the frontend, the infrastructure also uses [Vitest](https://vitest.dev/).
Unit tests should validate basic functionality as well as best practices, such
as the presence of tags.

#### Deploying to AWS

To deploy to AWS you need the [Pulumi](https://www.pulumi.com/) CLI and the the
[AWS CLI](https://aws.amazon.com/cli/) installed and configured.

Then you will need to run `pulumi up` for a stack other than dev.

## Managing issues and tasks

If you have a feature idea or a bug report, first search the existing issues in this repository to make sure it's not a duplicate. If it does not exist already, please create a new issue in this repository using one of the templates and set the "project" field to `agile-poker backlog`. Be sure to fill out all the information requested in the issue template. Do not create tasks directly on the project board.

If you want to work on a task:

1. Ensure it is in "Ready" status.
1. Open it from this repo, or if you open it from the project board click "Open in new tab".
1. Set the project status to "In progress". and click "Create a branch" in the "Development" section on the right. Check out the new branch locally and do your work on that branch.
1. When you are ready for your work to be reviewed, open a PR and complete the contributor checklist. Do not add the PR to the `agile-poker backlog` project.

