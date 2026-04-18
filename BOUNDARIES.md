# A2A-SIN-Zoom Boundaries

## Role
`A2A-SIN-Zoom` owns Zoom meeting/chat integration, session workflows, and Zoom-specific contracts.

## This repo should own
- Zoom meeting, chat, and session-support workflows
- Zoom evidence, recovery, auth, and session handling
- Zoom contracts used by downstream communication automation agents
- runbooks tied to meeting coordination, recording, and Zoom automation

## This repo must not own
- generic messaging ownership outside Zoom
- unrelated social, meeting, or chat platform behavior not tied to Zoom
- organization SSOT docs or architecture canon

## Hard rules
- Keep changes scoped to Zoom meeting/chat integration and session workflows.
- Move non-Zoom behavior back to the repos that own those surfaces.
- Keep reusable contracts focused on Zoom meetings, chat, and session automation.
