---
title: Install Vector On Raspbian
sidebar_label: Raspbian
description: Install Vector On Raspbian
---

This document will cover installing Vector on Raspbian.

## Install

<Tabs
block={true}
defaultValue="daemon"
values={[{"label":"As a Daemon","value":"daemon"}]}>
<TabItem value="daemon">

The [daemon deployment strategy][docs.strategies#daemon] is designed for data
collection on a single host. Vector runs in the background, in its own process,
collecting _all_ data for that host.
Typically data is collected from a process manager, such as Journald via
Vector's [`journald` source][docs.sources.journald], but can be collected
through any of Vector's [sources][docs.sources].
The following diagram demonstrates how it works.

<DaemonDiagram
  platformName={null}
  sourceName={null}
  sinkName={null} />

---

<Tabs
centered={true}
className={"rounded"}
defaultValue={"vector-cli"}
placeholder="Please choose an installation method..."
select={false}
size={null}
values={[{"group":"Nones","label":"Vector CLI","value":"vector-cli"},{"group":"Platforms","label":"Docker CLI","value":"docker-cli"},{"group":"Platforms","label":"Docker Compose","value":"docker-compose"}]}>
<TabItem value="vector-cli">

<Steps headingDepth={3}>
<ol>
<li>

### Install Vector

<InstallationCommand />

Or choose your [preferred method][docs.installation].

</li>
<li>

### Configure Vector

<ConfigExample
format="toml"
path={"vector.toml"}
sourceName={"journald"}
sinkName={null} />

</li>
<li>

### Start Vector

```bash
vector --config vector.toml
```

That's it! Simple and to the point. Hit `ctrl+c` to exit.

</li>
</ol>
</Steps>

</TabItem>
<TabItem value="docker-cli">

<Steps headingDepth={3}>
<ol>
<li>

### Configure Vector

<ConfigExample
format="toml"
path={"/etc/vector/vector.toml"}
sourceName={"journald"}
sinkName={null} />

</li>
<li>

### Start the Vector container

```bash
docker run \
  -v $PWD/vector.toml:/etc/vector/vector.toml:ro \
  timberio/vector:latest-alpine
```

<CodeExplanation>

- The `-v $PWD/vector.to...` flag passes your custom configuration to Vector.
- The `timberio/vector:latest-alpine` is the default image we've chosen, you are welcome to use [other image variants][docs.platforms.docker#variants].

</CodeExplanation>

That's it! Simple and to the point. Hit `ctrl+c` to exit.

</li>
</ol>
</Steps>

</TabItem>
<TabItem value="docker-compose">

compose!

</TabItem>
</Tabs>
</TabItem>
</Tabs>

[docs.installation]: /docs/setup/installation/
[docs.platforms.docker#variants]: /docs/setup/installation/platforms/docker/#variants
[docs.sources.journald]: /docs/reference/sources/journald/
[docs.sources]: /docs/reference/sources/
[docs.strategies#daemon]: /docs/setup/deployment/strategies/#daemon