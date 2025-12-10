# Portfolio-Optimization-Using-Linear-Algebra
Portfolio optimization using linear algebra, Markowitz efficient frontier modeling, and Monte Carlo simulation for performance validation.

# Overview

This project applies Modern Portfolio Theory (MPT), linear algebra, and Monte Carlo simulation to construct and validate optimized investment portfolios using 10 years of historical data.

The goal is to:

Build the unconstrained efficient frontier (short-selling allowed)

Build the long-only efficient frontier (weights ≥ 0)

Compute portfolios for different target returns using closed-form matrix algebra

Verify the model using Monte Carlo simulation

Visualize portfolio returns, volatilities, and weights

The portfolio universe includes 10 diversified asset classes, represented by the following ETFs and assets:

AGG	- U.S. Core Investment-Grade Bonds<br>
BTC-USD	- Bitcoin<br>
DBC	- Broad Commodities<br>
EEM	- Emerging Market Equities<br>
EFA	- Developed International Equities<br>
GLD	- Gold<br>
IJH	- U.S. Mid-Cap Equities<br>
IWM	- U.S. Small-Cap Equities<br>
SPY	- U.S. Large-Cap Equities<br>
VNQ	- U.S. Real Estate Investment Trusts (REITs)<br>

# Key Techniques Used
## Linear Algebra

Used to compute:

Log returns and annualized means

Covariance matrix

Closed-form Markowitz portfolio weights using

<img width="448" height="76" alt="Screenshot 2025-12-09 at 3 34 50 PM" src="https://github.com/user-attachments/assets/afbab97b-cc54-4c2d-9a81-9c1eb893f83a" />

where: 

<img width="208" height="144" alt="Screenshot 2025-12-09 at 3 36 38 PM" src="https://github.com/user-attachments/assets/5dbe81fe-0b08-4b81-9438-2229e7e98ab5" />

## Quadratic Optimization (Long-Only)

Inequality constraints 
𝑤 ≥ 0
w ≥ 0 prevent closed-form solutions.
Used CVXPY to solve:

<img width="482" height="35" alt="Screenshot 2025-12-09 at 3 38 11 PM" src="https://github.com/user-attachments/assets/dd40ef8a-fd6d-4027-b037-e7c0e0e045ca" />

## Monte Carlo Simulation

Simulated 10,000 market paths, 10 years each, using a multivariate normal distribution defined by μ and Σ.

Used simulation to verify:

Expected return matches theory

Volatility matches theory

Higher-return portfolios → higher volatility

# Project Workflow
## 1. Data Collection

Downloaded daily adjusted close prices using yfinance.

## 2. Data Cleaning

Removed rows with NaNs

Ensured synchronized trading dates across all assets

Computed log returns

## 3. Compute Portfolio Inputs

Annualized mean log returns (μ)

Annualized covariance matrix (Σ)

## 4. Build Efficient Frontier (Unconstrained)

Use closed-form matrix solution to compute weights

Construct portfolios for 50 target returns

## 5. Build Long-Only Frontier

Solve constrained quadratic program via CVXPY

Compare risk/return vs unconstrained frontier

## 6. Monte Carlo Verification

Simulated market paths to confirm:

Theoretical returns ≈ simulated returns

Theoretical volatility ≈ simulated volatility

Constrained frontier is less efficient (higher volatility per unit return)

# Mathematical Foundations

### Portfolio Return 
<img width="115" height="36" alt="Screenshot 2025-12-09 at 3 52 27 PM" src="https://github.com/user-attachments/assets/410be15f-4b1d-4f38-8e08-fab8de7a80d0" />

### Portfolio Variance
<img width="129" height="39" alt="Screenshot 2025-12-09 at 3 53 05 PM" src="https://github.com/user-attachments/assets/c432aa33-4b9f-4746-a9c5-70bc6d28c38b" />

### Closed-Form Minimum-Variance Portfolio (for target return)
<img width="440" height="76" alt="Screenshot 2025-12-09 at 3 53 41 PM" src="https://github.com/user-attachments/assets/634b53c3-3457-4218-adc8-b565436cc6b5" />

### Long-Only Optimization Problem
<img width="180" height="157" alt="Screenshot 2025-12-09 at 3 53 53 PM" src="https://github.com/user-attachments/assets/2ac0b0f4-c772-4c5b-8271-036cc605119a" />

# Monte Carlo Verification Summary
Simulated returns using μ and Σ from historical data

Applied each portfolio’s weight vector to all simulated paths

Computed mean and volatility across 10,000 paths

Results matched theoretical expectations

Confirms correctness of:

Covariance estimation

Closed-form weights

CVXPY optimization

Efficient frontier construction


