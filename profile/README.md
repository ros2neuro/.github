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
- 2026-05-05 [ltonin] **ros2neuro_training**, **ros2neuro_training_qt**: Added the initial C++/Qt decoder training scaffold with user-selectable preprocessing, feature, and decoder configuration.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Reworked the training GUI toward the old MATLAB layout with training setup and feature-selection views.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Modernized the import view for GDF runs with add/remove/clear controls, direct `libxdffileio` metadata/event inspection, compatibility checks, label overrides, and a topoplot placeholder.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Added GDF event pairing based on the convention that `code` opens an event and `code + 0x8000` closes it.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Added a Qt channel topoplot widget and switched displayed event codes to decimal.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Made the channel map an interactive pseudo-3D head view with mouse-drag rotation and responsive electrode sizing.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Updated the channel view so the head geometry, grid, nose, electrodes, and labels rotate together.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Changed the channel view default to an isometric head silhouette with ears, neck, and face ridge.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Replaced the painted channel view with a `QOpenGLWidget` procedural 3D head model and electrode spheres.
- 2026-05-05 [ltonin] **ros2neuro_training_qt**: Added runtime OBJ head mesh loading from `assets/head.obj`, with procedural fallback when no external model is installed.
- 2026-05-06 [ltonin] **ros2neuro_acquisition_gusbamp**: Updated g.USBamp reads for the new `libgusbampapi` byte-based `GT_GetSamplesAvailable`/`GT_GetData` contract and kept the C API private to the plugin implementation.
