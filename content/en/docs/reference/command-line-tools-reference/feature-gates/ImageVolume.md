---
title: ImageVolume
content_type: feature_gate
_build:
  list: never
  render: false

stages:
  - stage: alpha
    defaultValue: false
    fromVersion: "1.31"
    toVersion: "1.32"
  - stage: beta
    defaultValue: false
    fromVersion: "1.33"
---
Allow using the [`image`](/docs/concepts/storage/volumes/) volume source in a Pod.
This volume source lets you mount a container image as a read-only volume.
