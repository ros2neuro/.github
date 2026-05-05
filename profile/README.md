## ros2neuro

This organization hosts the ROS 2 packages for the ros2neuro ecosystem.

## Temporary changelog

This list is used temporarily to track changes made across the organization repositories.

- 2026-05-05 [ltonin] **ros2neuro_msgs**: Simplified `NeuroPrediction` to generic decoder output fields: `decoder`, `fields`, `values`, and `type`; removed hard classification index and added `TYPE_REGRESSION`.
- 2026-05-05 [ltonin] **ros2neuro_decoder**, **ros2neuro_decoder_lda**, **ros2neuro_decoder_svm**, **ros2neuro_decoder_qda**, **ros2neuro_decoder_gaussian**, **ros2neuro_integrator**, **ros2neuro_integrator_exponential**: Updated `NeuroPrediction` producers and consumers for the new generic message contract.
- 2026-05-05 [ltonin] **ros2neuro_decoder**, **ros2neuro_decoder_converters**, **ros2neuro_devel_test**: Updated decoder manifests to use `input` for the incoming `NeuroFeature` contract, `features` for the model feature set, and `output.fields` for prediction fields.
- 2026-05-05 [ltonin] **ros2neuro_decoder**, **ros2neuro_decoder_converters**, **ros2neuro_devel_test**: Added compact column-oriented decoder manifest selection syntax while keeping the explicit row-oriented syntax supported.
- 2026-05-05 [ltonin] **ros2neuro_msgs**: Replaced `NeuroDecision` with `NeuroControl` for processed decoder output used as continuous/discrete control signals.
- 2026-05-05 [ltonin] **ros2neuro_integrator**, **ros2neuro_integrator_exponential**, **ros2neuro_devel_test**: Updated integrator output to publish `NeuroControl` on the new control topic.
- 2026-05-05 [ltonin] **ros2neuro_acquisition_xdf**: Added optional XDF sensor/trigger group overrides for name, unit, labels, type, and value ranges via name-based or index-based parameters.
