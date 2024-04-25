
# LLM API Seqence Detection Results

This repo contains results for an experiment where we ran samples (both clean and malware) in an emulator, extracted the API call sequences for each sample, and then fed the sequences to 4 LLM models (llama2-13b, mistral, mixtral and mixtral-fp16).

## Response Length

Files [*mal_response_len.json*](mal_response_len.json), [*cln_response_len.json*](cln_response_len.json) and [*both_response_len.json*](both_response_len.json) contain the response lengths for the malware samples, clean samples and all samples respectively, grouped by each model.

Each file has the following format:

```json
{
    "model_name": {
        "sample_hash": "int response length"
    }
}
```


## Response durations

Files [*mal_durations.json*](mal_durations.json), [*cln_durations.json*](cln_durations.json) and [*both_durations.json*](both_durations.json) contain the response durations for the malware samples, clean samples and all samples respectively, grouped by each model.

Each file has the following format:

```json
{
    "model_name": {
        "sample_hash": "float duration in seconds"
    }
}
```

## Count of samples with 1, 2, 3 or 4 responses

Files [*mal_responses_count.json*](mal_responses_count.json), [*cln_responses_count.json*](cln_responses_count.json) and [*both_responses_count.json*](both_responses_count.json) contain the response counts for the malware samples, clean samples and all samples respectively. 

Each file has the following format:

```json
{
    "1": "int number of hashes for which only one model had a usable response",
    "2": "int number of hashes for which two models had usable responses",
    "3": "int number of hashes for which three models had usable responses",
    "4": "int number of hashes for which four models had usable responses"
    
}
```


## Models Performance

Files [*mal_models_stats.json*](mal_models_stats.json), [*cln_models_stats.json*](cln_models_stats.json) and [*both_models_stats.json*](both_models_stats.json) contain the stats for the malware samples, clean samples and all samples respectively, grouped by each model.

Each file has the following format:

```json
{
    "model_name": {
        "total_responses": "The total number of responses",
        "responses_with_match": "The total number of responses on which the regexes matched",
        "response_succes_rate": "The number of responses on which the regexes matched, divided by the total number of responses",
        "response_avg_duration": "The average duration of the responses (in seconds)",
        "total_duration": "The total time it took to get all responses from the models without retries due to errors or unusable responses(in seconds)",
        "avg_response_len": "The average response length of the models relative to the total number of responses",
    }
}
```

## Raw results

Files [*result_mal.json*](result_mal.json), [*result_cln.json*](result_cln.json) and [*result_both.json*](result_both.json) contain the raw results and duration for each prompt for the malware samples, clean samples and all samples respectively grouped by sample hash and model.

Each file has the following format:

```json
{
    "sample_hash": {
        "model_name": [
            {
                "response": "string",
                "duration": "float duration in seconds"
            }
        ]
    }
}
```


## Parsed results

Files [*match_result_mal.json*](match_result_mal.json), [*match_result_cln.json*](match_result_cln.json) and [*match_result_both.json*](match_result_both.json) contain the parsed results for the malware samples, clean samples and all samples respectively grouped by sample hash and model. 

Each file has the following format:

```json
{
    "sample_hash": {
        "model_name": [
            "digit"
        ]
    }
}
```

## Model performance comparison by threshold

File [*threshold_performance.json*](threshold_performance.json) contains the performance of the models for different thresholds. The thresholds are one of the following: 5,6,7,8,9. These thresholds are used to separate samples into malicious and clean when computing results. For each threshold, the results are grouped by model name. Besides the model name, we also used the average of the models to compute results.

The file has the following format: 

```json

{
    "threshold": {
        "model_name or average": {
            "FN": "int false negatives",
            "FP": "int false positives",
            "TN": "int true negatives",
            "TP": "int true positives",
            "accuracy": "float accuracy",
            "cln_samples": "int total clean samples",
            "det_rate": "float detection rate",
            "fp_rate": "float false positive rate",
            "mal_samples": "total malicious samples",
            "total_samples": "total samples"
        },

    }
}

```


## Leftover samples

Files [*leftover_mal.json*](leftover_mal.json), [*leftover_cln.json*](leftover_cln.json) and [*leftover_both.json*](leftover_both.json) contain the samples that did not yield matches when regexes were applied for the malware samples, clean samples and all samples respectively grouped by sample hash and model.

Files have the following format:

```json
{
    "sample_hash": {
        "model_name": [
            {
                "response": "string",
                "duration": "float duration in seconds"
            }
        ]
    }
}
```

## All samples

Finally, all sample hashes are in the [*all_hashes.json*](all_hashes.json) file in the form of a list of strings. All hashes are also available on https://virustotal.com for queries.

