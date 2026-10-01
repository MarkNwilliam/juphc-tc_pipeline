# juphc-tc_pipeline

Tekton pipeline for the Tax Calculator.

## Files

| File | What it is |
|---|---|
| `tekton/tasks.yaml` | The two new task definitions: `npminstall` (npm) and `tests` (Jasmine) |
| `tekton/pipeline.yaml` | Pipeline with steps `clone-source` -> `npminstall` -> `tests` -> `build` -> `push-image` / `deploy` |
| `tekton/run.yaml` | PipelineRun with apiVersion, kind, spec, params and workspaces |
| `tekton/tasks/` | Supporting task definitions: `clone-source`, `build`, `push-image`, `deploy` |

## Apply

```bash
oc apply -f tekton/tasks.yaml
for f in tekton/tasks/*.yaml; do oc apply -f "$f"; done
oc apply -f tekton/pipeline.yaml
oc apply -f tekton/run.yaml
```

All resources are `tekton.dev/v1` and validated against the v1.15.3 CRD schemas.
