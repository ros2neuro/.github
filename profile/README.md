## ros2neuro

This organization hosts the ROS 2 packages for the ros2neuro ecosystem.

## Temporary changelog

This list is used temporarily to track changes made across the organization repositories.

### ros2neuro_acquisition

- _No entries yet._

### ros2neuro_acquisition_antneuro

- _No entries yet._

### ros2neuro_acquisition_dummy

- _No entries yet._

### ros2neuro_acquisition_eegdev

- _No entries yet._

### ros2neuro_acquisition_gusbamp

- _No entries yet._

### ros2neuro_acquisition_xdf

- _No entries yet._

### ros2neuro_data

- _No entries yet._

### ros2neuro_decoder

- 2026-05-05: Updated `NeuroPrediction` consumers and documentation to use `decoder`, `fields`, `values`, and `type` instead of the previous hard-classification-oriented fields.

### ros2neuro_decoder_converters

- _No entries yet._

### ros2neuro_decoder_gaussian

- 2026-05-05: Updated Gaussian decoder prediction publishing and tests for the new generic `NeuroPrediction` message contract.

### ros2neuro_decoder_lda

- _No entries yet._

### ros2neuro_decoder_qda

- 2026-05-05: Updated QDA decoder prediction publishing and tests for the new generic `NeuroPrediction` message contract.

### ros2neuro_decoder_svm

- 2026-05-05: Updated SVM decoder prediction publishing and tests for the new generic `NeuroPrediction` message contract.

### ros2neuro_devel_test

- _No entries yet._

### ros2neuro_filters

- _No entries yet._

### ros2neuro_filters_blackman

- _No entries yet._

### ros2neuro_filters_butterworth

- _No entries yet._

### ros2neuro_filters_car

- _No entries yet._

### ros2neuro_filters_dc

- _No entries yet._

### ros2neuro_filters_flattop

- _No entries yet._

### ros2neuro_filters_hamming

- _No entries yet._

### ros2neuro_filters_hann

- _No entries yet._

### ros2neuro_filters_laplacian

- _No entries yet._

### ros2neuro_integrator

- 2026-05-05: Updated integrator consumers to read `NeuroPrediction.fields` and `NeuroPrediction.values`, deriving decisions from integrated values instead of decoder hard predictions.

### ros2neuro_integrator_exponential

- 2026-05-05: Updated exponential integrator to consume `NeuroPrediction.values` and `NeuroPrediction.type`.

### ros2neuro_msgs

- 2026-05-05: Simplified `NeuroPrediction` to generic decoder output fields: `decoder`, `fields`, `values`, and `type`; removed hard classification index and added `TYPE_REGRESSION`.

### ros2neuro_processing_spectral

- _No entries yet._

### ros2neuro_recorder

- _No entries yet._

### ros2neuro_recorder_xdf

- _No entries yet._

### ros2neuro_visualizer

- _No entries yet._
