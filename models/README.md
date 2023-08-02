**low-bias:** normal 1-step fine-tuning using Roboflow's data with the best MAP score

**conservative:** 2-step fine-tuning looking for a configuration that would detect more apples in the sample image, with 2nd best MAP score

**high-bias:** 3-step fine-tuning for the best configuration that would detect 41 apples in the sample image, with the 3rd best MAP score (but not far from the other two models)

Because there is no proper test data provided within the scope of this work, only a singular sample, then tuning towards good performance for only this singular image would potentially result in a biased model (hence the name).
In a real AI-in-production scenario, there should be test data, or in this case, if we borrow Roboflow's val data as the test data, then the more robust model can be the low-bias model until we have new information.
