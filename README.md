# Stock-Price-Prediction


## AIM

To develop a Recurrent Neural Network model for stock price prediction.

## Problem Statement and Dataset
Predicting stock prices is a complex task due to market volatility. Using historical closing prices, we aim to develop a Recurrent Neural Network (RNN) model that can analyze time-series data and generate future price predictions.

## Design Steps

### Step 1:
Data Collection & Preprocessing: Load historical stock prices, normalize using MinMaxScaler, and create sequences for time-series input.
### Step 2:
Model Design: Build an RNN with two layers, define input/output sizes, and set activation functions.
### Step 3:
Training Process: Train the model using MSE loss and Adam optimizer for 20 epochs with batch-size optimization.
### step 4:
Evaluation & Prediction: Test on unseen data, inverse transform predictions, and compare with actual prices.
### step 5:
Visualization & Interpretation: Plot training loss and predictions to analyze performance and potential improvements.

## Program
#### Name: Gokularamanan K
#### Register Number: 212222230040
Include your code here
```Python 
# Define RNN Model
class RNNModel(nn.Module):
  def __init__(self, input_size=1, hidden_size=64, num_layers=2, output_size=1):
    super(RNNModel, self).__init__()
    self.rnn = nn.RNN(input_size, hidden_size, num_layers, batch_first = True)
    self.fc = nn.Linear(hidden_size, output_size)

  def forward(self,x):
    out, _ = self.rnn(x)
    out = self.fc(out[:, -1, :])
    return out

model = RNNModel()
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model = model.to(device)


# Train the Model
epochs = 20
model.train()
train_losses = []
for epoch in range(epochs):
  epoch_loss = 0
  for x_batch, y_batch in train_loader:
    x_batch, y_batch = x_batch.to(device), y_batch.to(device)
    optimizer.zero_grad()
    outputs = model(x_batch)
    loss = criterion(outputs, y_batch)
    loss.backward()
    optimizer.step()
    epoch_loss += loss.item()
  train_losses.append(epoch_loss / len(train_loader))
  print(f"Epoch [{epoch+1}/{epochs}], Loss:{train_losses[-1]:.4f}")

```

## Output

### True Stock Price, Predicted Stock Price vs time
![image](https://github.com/user-attachments/assets/1b8b2af7-5f68-45a9-a2c1-8f167b27146c)




### Predictions 
![image](https://github.com/user-attachments/assets/11bc5b9d-3ba4-4d60-9510-17958d7ca904)




## Result
The RNN model effectively forecasts future stock prices using historical closing data. The predicted values closely align with actual prices, showcasing the model's ability to recognize temporal trends. Performance evaluation is conducted by visually comparing predicted and actual prices through plotted graphs.



