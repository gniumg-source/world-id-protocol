From 33821f899284ed51dc0ea9437c5f36ddbbc006d3 Mon Sep 17 00:00:00 2001
From: "github-actions[bot]"
 <41898282+github-actions[bot]@users.noreply.github.com>
Date: Fri, 6 Mar 2026 23:39:57 +0000
Subject: [PATCH] chore: release v0.5.1

---
 CHANGELOG.md              | 11 +++++++++++
 Cargo.lock                | 14 +++++++-------
 Cargo.toml                | 14 +++++++-------
 services/relay/Cargo.toml |  2 +-
 4 files changed, 26 insertions(+), 15 deletions(-)

diff --git a/CHANGELOG.md b/CHANGELOG.md
index 0ebc261e..148ad16a 100644
--- a/CHANGELOG.md
+++ b/CHANGELOG.md
@@ -7,6 +7,17 @@ and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0
 
 ## [Unreleased]
 
+## [0.5.1](https://github.com/gniumg-source/world-id-protocol/compare/world-id-primitives-v0.5.0...world-id-primitives-v0.5.1) - 2026-03-06
+
+### Added
+
+- structured timeout errors ([#532](https://github.com/gniumg-source/world-id-protocol/pull/532))
+- in-flight locks for all gateway operations ([#519](https://github.com/gniumg-source/world-id-protocol/pull/519))
+
+### Fixed
+
+- *(indexer)* prevent panics in inclusion-proof handler ([#529](https://github.com/gniumg-source/world-id-protocol/pull/529))
+
 ## [0.5.0](https://github.com/worldcoin/world-id-protocol/compare/world-id-primitives-v0.4.4...world-id-primitives-v0.5.0) - 2026-03-03
 
 ### Added
diff --git a/Cargo.lock b/Cargo.lock
index 8d42a4ca..3d6ced22 100644
--- a/Cargo.lock
+++ b/Cargo.lock
@@ -3487,7 +3487,7 @@ checksum = "42012b0f064e01aa58b545fe3727f90f7dd4020f4a3ea735b50344965f5a57e9"
 
 [[package]]
 name = "generate-solidity-fixtures"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "alloy",
  "eyre",
@@ -8798,7 +8798,7 @@ dependencies = [
 
 [[package]]
 name = "world-id-authenticator"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "alloy",
  "anyhow",
@@ -8827,7 +8827,7 @@ dependencies = [
 
 [[package]]
 name = "world-id-core"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "alloy",
  "backon",
@@ -8955,7 +8955,7 @@ dependencies = [
 
 [[package]]
 name = "world-id-issuer"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "alloy",
  "ark-ff 0.5.0",
@@ -9036,7 +9036,7 @@ dependencies = [
 
 [[package]]
 name = "world-id-primitives"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "alloy",
  "alloy-primitives",
@@ -9073,7 +9073,7 @@ dependencies = [
 
 [[package]]
 name = "world-id-proof"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "ark-bn254 0.5.0",
  "ark-ec 0.5.0",
@@ -9100,7 +9100,7 @@ dependencies = [
 
 [[package]]
 name = "world-id-relay"
-version = "0.5.0"
+version = "0.5.1"
 dependencies = [
  "alloy",
  "alloy-primitives",
diff --git a/Cargo.toml b/Cargo.toml
index 9eb1744c..1dce1e81 100644
--- a/Cargo.toml
+++ b/Cargo.toml
@@ -20,7 +20,7 @@ resolver = "2"
 
 [workspace.package]
 edition = "2024"
-version = "0.5.0"
+version = "0.5.1"
 license = "MIT"
 authors = [
   "World Foundation",
@@ -127,12 +127,12 @@ tokio-util = "0.7"
 tower = "0.5.3"
 
 # Internal
-world-id-core = { version = "0.5.0", default-features = false, path = "crates/core" }
-world-id-issuer = { version = "0.5.0", path = "crates/issuer" }
-world-id-proof = { version = "0.5.0", path = "crates/proof" }
-world-id-authenticator = { version = "0.5.0", path = "crates/authenticator" }
-world-id-primitives = { version = "0.5.0", path = "crates/primitives", default-features = false }
+world-id-core = { version = "0.5.1", default-features = false, path = "crates/core" }
+world-id-issuer = { version = "0.5.1", path = "crates/issuer" }
+world-id-proof = { version = "0.5.1", path = "crates/proof" }
+world-id-authenticator = { version = "0.5.1", path = "crates/authenticator" }
+world-id-primitives = { version = "0.5.1", path = "crates/primitives", default-features = false }
 world-id-oprf-node = { version = "0.1.0", path = "services/oprf-node" }
 world-id-test-utils = { version = "0.1.0", path = "crates/test-utils" }
 world-id-services-common = { path = "services/common" }
-world-id-relay = { path = "services/relay" }
\ No newline at end of file
+world-id-relay = { path = "services/relay" }
diff --git a/services/relay/Cargo.toml b/services/relay/Cargo.toml
index 2d339e8b..b3d34ece 100644
--- a/services/relay/Cargo.toml
+++ b/services/relay/Cargo.toml
@@ -45,4 +45,4 @@ eyre = { workspace = true }
 config = { workspace = true }
 
 [dev-dependencies]
-world-id-relay = { workspace = true }
\ No newline at end of file
+world-id-relay = { workspace = true }
