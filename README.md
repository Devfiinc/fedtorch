# Federated Learning with Flower and PyTorch

Two clients and one server.

Start the process running below instructions in three different terminals:

```bash
python server.py
python client.py
python client.py
```

The model will begin training with the 2 clients:

 - At any given time I can start a new client, and it will remain idle and ready until current training loop ends, at that time it will join the training process.

 - Similarly, I can stop a client during the process, forcing it to leave the environment at once, so after the training is completed in the remaining clients the server will only aggregate the models of the surviving ones.

In our implementation, an Actor will be overseeing each of the elements (server & clients), also a new actor will be attached to any new client that joins the environment. Alternativelly maybe our end app (installed) in the new clients already creates an actor when initializing.

See below the logs of the server:


```bash
INFO flower 2022-11-02 10:47:21,297 | app.py:131 | Starting Flower server, config: ServerConfig(num_rounds=3, round_timeout=None)
INFO flower 2022-11-02 10:47:21,309 | app.py:144 | Flower ECE: gRPC server running (3 rounds), SSL is disabled
INFO flower 2022-11-02 10:47:21,309 | server.py:86 | Initializing global parameters

INFO flower 2022-11-02 10:47:21,310 | server.py:270 | Requesting initial parameters from one random client
INFO flower 2022-11-02 10:50:10,476 | server.py:274 | Received initial parameters from one random client
INFO flower 2022-11-02 10:50:10,476 | server.py:88 | Evaluating initial parameters
INFO flower 2022-11-02 10:50:10,477 | server.py:101 | FL starting

DEBUG flower 2022-11-02 10:52:59,046 | server.py:215 | fit_round 1: strategy sampled 2 clients (out of 2)
DEBUG flower 2022-11-02 10:55:36,269 | server.py:229 | fit_round 1 received 2 results and 0 failures
DEBUG flower 2022-11-02 10:55:36,274 | server.py:165 | evaluate_round 1: strategy sampled 2 clients (out of 2)
DEBUG flower 2022-11-02 11:10:37,440 | server.py:179 | evaluate_round 1 received 2 results and 0 failures

DEBUG flower 2022-11-02 11:10:37,440 | server.py:215 | fit_round 2: strategy sampled 3 clients (out of 3)
DEBUG flower 2022-11-02 11:15:25,514 | server.py:229 | fit_round 2 received 2 results and 1 failures
DEBUG flower 2022-11-02 11:15:25,517 | server.py:165 | evaluate_round 2: strategy sampled 2 clients (out of 2)
DEBUG flower 2022-11-02 11:31:04,761 | server.py:179 | evaluate_round 2 received 2 results and 0 failures

DEBUG flower 2022-11-02 11:31:04,761 | server.py:215 | fit_round 3: strategy sampled 2 clients (out of 2)
DEBUG flower 2022-11-02 11:34:38,584 | server.py:229 | fit_round 3 received 2 results and 0 failures
DEBUG flower 2022-11-02 11:34:38,588 | server.py:165 | evaluate_round 3: strategy sampled 2 clients (out of 2)
DEBUG flower 2022-11-02 11:48:10,748 | server.py:179 | evaluate_round 3 received 2 results and 0 failures

INFO flower 2022-11-02 11:48:10,748 | server.py:144 | FL finished in 3480.271497940994
INFO flower 2022-11-02 11:48:10,748 | app.py:192 | app_fit: losses_distributed [(1, 2.1023998260498047), (2, 1.675815224647522), (3, 1.5115591287612915)]
INFO flower 2022-11-02 11:48:10,748 | app.py:193 | app_fit: metrics_distributed {'accuracy': [(1, 0.2439), (2, 0.3882), (3, 0.448)]}
INFO flower 2022-11-02 11:48:10,748 | app.py:194 | app_fit: losses_centralized []
INFO flower 2022-11-02 11:48:10,748 | app.py:195 | app_fit: metrics_centralized {}

```