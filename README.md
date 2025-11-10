🧠 Research & Development / AI — Parametric Curve Estimation
📄 Problem Statement

Find the unknown parameters in the given parametric equation of a curve:
x=(t⋅cos(θ)−eM∣t∣⋅sin(0.3t)sin(θ)+X)
y=(42+t⋅sin(θ)+eM∣t∣⋅sin(0.3t)cos(θ))
where the unknowns are:
θ,M,X
🔢 Given Ranges
0∘<θ<50∘,−0.05<M<0.05,0<X<100
6<t<60
The provided dataset (xy_data.csv) contains (x,y) points on the curve for 6<t<60.

🎯 Objective

Estimate the parameters θ, M, and 𝑋 such that the L₁ distance between the predicted and observed points is minimized:
L1​=N1​i∑​(∣xi​−xi​^​∣+∣yi​−yi​^​∣)
⚙️ Approach and Steps
Step 1: Load the Data

The CSV file xy_data.csv was loaded using pandas.

The dataset contained two columns: x and y.

The parameter t was uniformly sampled between 6 and 60 based on the number of data points.

Step 2: Define the Parametric Model
def model(t, theta, M, X):
    theta = np.deg2rad(theta)
    A = np.exp(M*np.abs(t)) * np.sin(0.3*t)
    x = t*np.cos(theta) - A*np.sin(theta) + X
    y = 42 + t*np.sin(theta) + A*np.cos(theta)
    return x, y
Step 3: Define the Error Function

The L₁ distance was used as the loss metric:
def l1_error(theta, M, X):
    x_pred, y_pred = model(t, theta, M, X)
    return np.mean(np.abs(x_data - x_pred) + np.abs(y_data - y_pred))
    Step 4: Random + Local Search Optimization

Global random search: 5000 random combinations of parameters within the given range.

Local refinement: Gaussian sampling around the best found parameters to further reduce error.

Step 5: Output and Visualization

The best-fit parameters were found and used to generate a comparison plot between actual and predicted data.

🧮 Results
| Parameter               | Symbol | Estimated Value |
| ----------------------- | ------ | --------------- |
| Angle                   | θ      | **28.298°**     |
| Exponential coefficient | M      | **0.022377**    |
| Translation constant    | X      | **54.8974**     |
Minimum L₁ Error: ≈ 25.24

🧾 Final Equation (Submission Format)
(tcos(28.2983)−e(0.022377∣t∣)sin(0.3t)sin(28.2983)+54.8974,42+tsin(28.2983)+e(0.022377∣t∣)sin(0.3t)cos(28.2983))


🚀 How to Run (Google Colab)

Open Google Colab

Upload xy_data.csv

Paste contents of fit_parametric_curve.py

Run all cells

Output will display:

Optimized parameters (θ, M, X)

L₁ error

Equation in submission format

Curve fitting plot
