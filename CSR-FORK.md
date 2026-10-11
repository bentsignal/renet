# CSGO Rewrite transport integration fork

This fork retains Renet's original authors and MIT/Apache-2.0 licenses.
CSGO Rewrite pins a specific revision rather than tracking this branch.

The integration patch validates fragment indices before reconstruction,
rejects inconsistent fragment counts within a message, checks allocation
arithmetic, validates unreliable payload sizes, and returns channel errors
instead of indexing outside allocated storage. Tests cover invalid indices,
inconsistent counts, allocation overflow, and packet loss/reordering.

The netcode.io socket adapters add `update_with_packet_limit` for hosts that
need a finite receive budget before advancing a fixed-tick simulation.
Existing `update` behavior is unchanged. Loopback tests verify excess UDP
datagrams remain available for a later update.

The fork's CI tests and lints the modified `renet` and `renet_netcode` crates;
it does not build the unrelated Bevy/Steam demonstration applications.
