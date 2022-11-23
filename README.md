# Aalto_PhD_task
Solution to task given by research group in Aalto University for PhD position in "Physics Driven Machine Learning and Quantum Computing"
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% writeLaTeX Example: Academic Paper Template
%
% Source: http://www.writelatex.com
% 
% Feel free to distribute this example, but please keep the referral
% to writelatex.com
% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% How to use writeLaTeX: 
%
% You edit the source code here on the left, and the preview on the
% right shows you the result within a few seconds.
%
% Bookmark this page and share the URL with your co-authors. They can
% edit at the same time!
%
% You can upload figures, bibliographies, custom classes and
% styles using the files menu.
%
% If you're new to LaTeX, the wikibook is a great place to start:
% http://en.wikibooks.org/wiki/LaTeX
%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\documentclass[twocolumn,showpacs,%
  nofootinbib,aps,superscriptaddress,%
  eqsecnum,prd,notitlepage,showkeys,10pt]{revtex4-1}

\usepackage{amssymb}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{dcolumn}
\usepackage{hyperref}
\usepackage{float}

\usepackage{mathtools}
\DeclarePairedDelimiter\bra{\langle}{\rvert}
\DeclarePairedDelimiter\ket{\lvert}{\rangle}
\DeclarePairedDelimiterX\braket[2]{\langle}{\rangle}{#1 \delimsize\vert #2}


\begin{document}

\title{Assignment }
\author{Aalto University - PhD Position on \\"Physics Driven Machine Learning and Quantum Computing"}
\maketitle
\texttt{\section{Ornstein–Uhlenbeck process}}
Aim : To study the given scalar stochastic differential equation, finding its solutions and plotting its trajectories.\\
\begin{center}
    $ \frac{dx(t)}{dt} = -\lambda x(t) + \omega(t) $, $x(0) = x_{0}$ 
\end{center}
\texttt{\subsection{Complete Solution of SDE}}
The above Linear Non-homogeneous Stochastic differential equation can be solved by multiplying an Integrating Factor (I.F.) on both the sides of the equation\cite{sarka}. We'll take the I.F. as $ e^{\lambda t} $ so that we can modify the equation to our benefit. \\

$e^{\lambda t} \frac{dx(t)}{dt} + e^{\lambda t} \lambda x(t) = e^{\lambda t} \omega(t) $\\

The LHS can be seen as a differential of product of two functions. So the equation can be simplified as :\\

$d(e^{\lambda t} x(t)) = e^{\lambda t} \omega(t) dt$ \\

$e^{\lambda t} x(t) - x_{0} = \int_0^t e^{\lambda \tau} \omega(\tau) \, d\tau $ \\
\begin{center}
$ \boxed{ x(t) = e^{-\lambda t} x_{0} + \int_0^t e^{\lambda (\tau - t)} \omega(\tau) \, d\tau }$
\end{center}

The mean $m(t)$ can be found by taking the expectation of the above equation. White noise $ \omega (t)$ is described as a Gaussian process with zero mean \cite{sarka}, therefore the second term in x(t) vanishes when we take expectation.
\begin{center}$
    \boxed
        {E[x(t)] = e^{-\lambda t} x_{0} = m(t)  } $
\end{center}
The variance $P(t)$ is described by the following relation \cite{sarka} :

$ P(t) = E[(x(t)-m(t))(x(t)-m(t))^{T}]$ \\



$=E[ (e^{-\lambda t} (x_{0}-x_{0}) + \int_0^t e^{\lambda (\tau - t)} \omega(\tau) \, d\tau) ((x_{0}-x_{0})^{T} (e^{- \lambda t})^{T} + \int_0^t \omega^{T}(\tau) (e^{\lambda (\tau-t)})^{T} \, d\tau) ]$ \\ 

$=E[ ( \int_0^t e^{\lambda (\tau - t)} \omega(\tau) \omega^{T}(\tau) (e^{\lambda (\tau-t)})^{T} \, d\tau ] $ \\


$=\int_0^t q e^{2\lambda (\tau-t)} \, d\tau  $ \\
 
We simplified the equation by using the Dirac delta correlation of white noise $E[\omega(t) \omega^{T}(s)] = \delta(t-s)q$ \\
where q is the spectral density. \\

On integrating P(t) we get : 
\begin{center}
    $\boxed{P(t) = \frac{q}{2\lambda}(1-e^{-2\lambda t}) }$
\end{center}


\subsection{Calculating Limits of Mean and Variance}
From our previous calculations, we know that\\
$ m(t) = e^{-\lambda t} x_{0}$ \\
At t \rightarrow \infty, \hspace{6} $e^{-\lambda t}$ will be very small and can be approximated to zero
\begin{center}
   \boxed{$ lim_{t\rightarrow \infty } m(t) = 0$ }
\end{center}
By the same logic let us now find out P(t) at $t \rightarrow \infty$ .\\
$P(t) = \frac{q}{2\lambda} (1 - e^{-2 \lambda t})$ \\ 
\begin{center}
\boxed{
$ lim_{t \rightarrow \infty}P(t) =  \frac{q}{2 \lambda} $}\\
\end{center}
Let us now find the mean and variance by solving the stationary state of the differential equations

$\frac{dm}{dt} = 0$ and $\frac{dP}{dt} = 0$ \\ 

$m(t) = e^{-\lambda t} x_{0}$ \\

$\frac{dm}{dt} = -\lambda e^{-\lambda t} x_{0} $ \\

$ \frac{dm}{dt} = -\lambda m(t) = 0$\\

\textbf{gives m(t) = 0}. Similarly, \\

$\frac{dP}{dt} = 2 \lambda ( \frac{q}{2\lambda} e^{-2\lambda t}) = 0 $ \\

Adding and subtracting terms to get the equation in terms of P(t) \\

$\frac{dP}{dt} = \frac{q}{2\lambda} e^{-2\lambda t} -\frac{q}{2\lambda} + \frac{q}{2\lambda} = 0 $\\

$\frac{dP}{dt} = \frac{q}{2\lambda} (e^{-2\lambda t} - 1) + \frac{q}{2\lambda} = 0 $\\

$\frac{dP}{dt} = \frac{q}{2\lambda} (1 - e^{-2\lambda t}) = \frac{q}{2\lambda} $\\

\textbf{gives $ P(t) = \frac{q}{2\lambda}$}

\subsection{Trajectories}

To simulate trajectories we will use the Euler-Maruyama Method which is a modified version of Euler method applied on our Stochastic ODE. \cite{sarka}\cite{oksendal} \\

$ \Delta x = -\lambda x(t) \Delta t + \omega(t) \Delta t$ \\

$x_{k+1} = x_{k} - \lambda x_{k} \Delta t + \omega (t) \Delta t$ \\

$\omega (t) \Delta t$ can be replaced by a Gaussian random variable with distribution N(0, $q \Delta t$) where q is the spectral density. \\
Using this equation we simulate 1000 trajectories and plot them corresponding to time. 

\begin{figure}[H]
\includegraphics[width=5cm, height=3.2cm]{trajectories.png}
\centering
\caption{\label{fig:traj}Plotting 1000 trajectories of the system. \\
\textit{The black line represents the noise-free mean trajectory m(t) and the red line represents the variance P(t).}}
\end{figure}
We know that $ m(t) = e^{-\lambda t} x_{0}, $ for $ x_{0} = 1$ and $\lambda = \frac{1}{2}$, lies between 0.6 to 1 which is approximately correct for the mean trajectory shown in the above plot.\\
Similarly, P(t) ranges from 0 to 0.4 which is again coherent with the results we have got in the plot. The difference in the accuracy of these trajectories is because we have used an approximate method which is bound to give deflected values.  \\
The mean and variance trajectories look like straight lines in the given time range, but if we consider a longer duration we can easily see that the graphs are exponential. 
\begin{figure}[H]
\includegraphics[width=5cm, height=3.2cm]{exponential_graphs.png}
\centering
\caption{\label{fig:your-figure}Plotting 20 trajectories of the system for time range 0 to 50 units.}
\end{figure}

Hence, we can say that the behaviour of mean and variance trajectory is in accordance with the theoretical values we calculated. 
\section{HHL Algorithm}
Aim : To solve the following set of linear equations through Classical (Gaussian elimination and NumPy) and Quantum (HHL: Qiskit) methods and compare the results.
\begin{center}
$ x - \frac{1}{4} y = 4$ \\

$ -\frac{1}{4} x - y = 0$
\end{center}
\label{sec:examples}
\subsection{Canonical Form}
The set of above given linear equations can be translated to a vector equation including a matrix A, vector x and constant vector b where  
$A = $$\begin{bmatrix} 1 & -1/4 \\ -1/4 & 1 \end{bmatrix}$$ $ , $\vec{x} = $$\begin{bmatrix} x \\ y \end{bmatrix}$$ $ and $\vec{b} = $$\begin{bmatrix} 4 \\ 0 \end{bmatrix}$$ $, such that we can write the set of linear equations as A $\vec{x}$ = $\vec{b}$\\
\begin{center}
$ $$\begin{bmatrix} 1 & -1/4 \\ -1/4 & 1 \end{bmatrix}$$ $$\begin{bmatrix} x \\ y \end{bmatrix}$$ = $$\begin{bmatrix} 4 \\ 0 \end{bmatrix}$$ $
\end{center}

\subsection{Gaussian elimination}
Now we solve the vector equation using the Gaussian Elimination Method. The motive is to obtain an identity matrix from the A matrix by applying row operations like swap, scalar multiplication and addition on the system. This would leave the variables x, y on the LHS and their values in the modified b vector. \\
Let's apply some row operations on the following system :

$\left[
\begin{array}{cc|c}
1 & -1/4 & 4 \\
-1/4 & 1 & 0\\
\end{array}
\right]$  

\begin{center}$ R _{2} \rightarrow R _{2} + \frac{1}{4} R _{1} $ \end{center}

$\left[
\begin{array}{cc|c}
1 & -1/4 & 4 \\
0 & \frac{15}{16} & 1\\
\end{array}
\right]$

\begin{center} $ R _{1} \rightarrow R _{1} + \frac{4}{15} R _{2} $ \end{center}


$\left[
\begin{array}{cc|c}
1 & 0 & \frac{64}{15} \\
0 & \frac{15}{16} & 1\\
\end{array}
\right]$

\begin{center} $ R _{2} \rightarrow \frac{16}{15} R _{2} $ \end{center}

$\left[
\begin{array}{cc|c}
1 & 0 & \frac{64}{15} \\
0 & 1 & \frac{16}{15}\\
\end{array}
\right]$ \\

This system translates to the following equation
\begin{center} 
$ $$\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$ $$\begin{bmatrix} x \\ y \end{bmatrix}$$ = $$\begin{bmatrix} \frac{64}{15} \\ \frac{16}{15} \end{bmatrix}$$ $ \end{center}
which implies that $\textbf{x = $\frac{64}{15}$}$ and $\textbf{y = $\frac{16}{15}$}$


\hfill \break 
% Use \texttt{section}s and \texttt{subsection}s to organize your document. \LaTeX{} handles all the formatting and numbering automatically. Use \texttt{ref} and \texttt{label} for cross-references --- this is Section~\ref{sec:examples}, for example.
\subsection{HHL Algorithm : Working}

In this section we will use the HHL algorithm to find the solution vector to the given linear equations. For an equation $A \vec{x} = \vec{b}$, with sparse A having a small condition number, this algorithm can find a function of $\vec{x}$, in run-time of ploy(log(N)) as compared to the fastest classical algorithms of run-time $N\sqrt{\kappa}$.\cite{hhlpaper} It uses the Quantum Phase Estimation method to get information on the eigenvalues of A and using them to apply unitary operators on the state $\ket{b}$. \\
Note that the matrix A is hermitian. So, we will be using it's spectral decomposition, as given below, in the calculations.\cite{qiskit} \\

$A=\sum_{j=0}^{N-1}\lambda_{j}|u_{j}\rangle\langle u_{j}|,\quad \lambda_{j}\in\mathbb{ R }$\\

The state $\ket{b}$ and $\ket{x}$ can also be written in a similar form. Note that $\ket{b}$ is expressed in the eigenbasis of A. \\

$|b\rangle=\sum_{j=0}^{N-1}b_{j}|u_{j}\rangle,\quad b_{j}\in\mathbb{ C }$\\ 

$ |x\rangle=A^{-1}|b\rangle=\sum_{j=0}^{N-1}\lambda_{j}^{-1}b_{j}|u_{j}\rangle$\\

We will use three sets of quantum registers : $n_{l}$, $n_{b}$, $n_{a}$. $n_{l}$ stores the binary representation of the eigenvalues of A. So, the bigger the matrix, more the number of qubits/quantum registers will be required. $n_{b}$ contains the vector solution and it is the set of qubits where the quantum state $\ket{b}$ is loaded. All the other qubits are auxiliary qubits and are required for other intermediate steps. Given below is a circuit diagram for the HHL algorithm. 

\begin{figure}[H]
\includegraphics[width=9cm, height=4.5cm]{hhl_algo.png}
\centering
\caption{\label{fig:your-figure}Workflow of the HHL algorithm.\\ \textit{Source : Qiskit Notebook \cite{qiskit}}}
\end{figure}
Here is the workflow of the algorithm \cite{qiskit}:
\begin{enumerate}
  \item First we load the state $ \ket{b}$ in the circuit. \\ $|0\rangle _{n_{b}} \mapsto |b\rangle _{n_{b}}$
  \item Applying Quantum Phase Estimation on $ \ket{b}$. \\
  
  $U = e ^ { i A t } := \sum _{j=0}^{N-1}e ^ { i \lambda _ { j } t } |u_{j}\rangle\langle u_{j}| $ \\
  
  The obtained state can be written in the eigenbasis of A as : \\
  
  $ \sum_{j=0}^{N-1} b _ { j } |\lambda _ {j }\rangle_{n_{l}} |u_{j}\rangle_{n_{b}}$
  \item We then add an auxiliary qubit to the circuit and apply a gate which is a function of $\ket{\lambda_{j}} $ such that we receive the following state. \\
  
  $ \sum_{j=0}^{N-1} b _ { j } |0\rangle_{n_{l}}|u_{j}\rangle_{n_{b}} \left( \sqrt { 1 - \frac {C^{2}  } { \lambda _ { j } ^ { 2 } } } |0\rangle + \frac { C } { \lambda _ { j } } |1\rangle \right)$
  \item Now, we measure the auxiliary qubit in the computational basis. If the output is 1, then we can extract the quantum state $ |x\rangle=A^{-1}|b\rangle=\sum_{j=0}^{N-1}\lambda_{j}^{-1}b_{j}|u_{j}\rangle$ from the system state which now looks like this : \\
  
  $ \left( \sqrt { \frac { 1 } { \sum_{j=0}^{N-1} \left| b _ { j } \right| ^ { 2 } / \left| \lambda _ { j } \right| ^ { 2 } } } \right) \sum _{j=0}^{N-1} \frac{b _ { j }}{\lambda _ { j }} |0\rangle_{n_{l}}|u_{j}\rangle_{n_{b}}$
  \item We can now apply any observable M and measure the state stored in $ n_{b}$ to to find it's expectation value.\\ 
  
\end{enumerate}

\subsection{Simulating HHL}
In this section we write a program to calculate the solution vector using the numpy.linalg.solve() method and the HHL method. We then compare these two results.\\
We see that using NumPy we get\\
numpy vec = $[[4.26666667],[1.06666667]]$\\
with a norm of 4.3979. \\

The HHL algorithm as used from the qiskit.algorithms library implemented the following quantum circuit. \\
\begin{figure}[H]
\includegraphics[width=8cm, height=3.5cm]{hhl_qc.png}
\centering
\caption{\label{fig:your-figure}HHL Quantum Circuit.\\
\textit{Note that the circuit doesn't measure the auxiliary qubit for us and that the operators are applied on different qubits compared to the circuit we used in the explanation part. (FIG. 2.). So, we will have to figure out the auxiliary qubit to flag and the set of qubits to read in order to get the solution vector.}}
\end{figure}
\\

If it were a real quantum computer, we could have measured the auxiliary qubit and then proceeded in either of the two ways. First, by measuring the remaining quantum state a large number of times so as to get the solution vector. This method is not feasible as the quantum state collapses on measurement and it would consume a lot of resources to generate the state and measure it multiple times. The second way can be used to find an estimate to the expectation value of an operator associated with $ \ket{x}$, which is the way the original HHL algorithm works.\\

As we are working on a quantum simulator, it can give us insights of the obtained state without having to measure it. We will be using Qiskit's Statevector simulator to get the required solution vector \vec{x}. 

\begin{figure}[H]
\includegraphics[width=9cm, height=2cm]{code_hhl_sv.png}
\centering
\caption{\label{fig:your-figure}Extracting x vector from HHL solution\\
\textit{Here we show how the Statevector function can be used to obtain the quantum state of interest. Note that the resultant state is not normalised. The state also has a complex part, but as it is very small, we will be ignoring it.}}
\end{figure}

We now normalize the vectors obtained from the classical and quantum methods and compare them.\\ 
\textbf{Normalised NumPy vector:}  [0.9701425 0.24253563]\\
and \\
\textbf{Normalised HHL vector:} [0.95085646 0.30963202] \\

We can see that the HHL algorithm has managed to make a good estimate of the $\vec{x}$. The accuracy of results depends on the number of qubits we use to store the eigenvalue of the A matrix.\cite{improvhhl} Hence, it can be improved by adding more qubits to the circuit. 
\section{References} 
\begin{thebibliography}{9}
\bibitem{sarka}
S. S ̈arkk ̈a and A. Solin, Applied Stochastic Differential Equations. Cam-bridge University Press, 2019.

\bibitem{oksendal}
Øksendal, B. K. (Bernt Karsten), 1945-. Stochastic Differential Equations : an Introduction with Applications. Berlin ; New York :Springer, 2003.

\bibitem{hhlpaper}
A. W. Harrow, A. Hassidim, and S. Lloyd, “Quantum algorithm for linear systems of equations,” Physical Review Letters, vol. 103, no. 15, p. 150502, 2009.

\bibitem{qiskit}
M. S. ANIS, Abby-Mitchell, H. Abraham, et al., “Qiskit: An open-source framework for quantum computing,” 2021.

\bibitem{improvhhl}
An Iterative Improvement Method for HHL
algorithm for Solving Linear System of Equations - https://arxiv.org/abs/2108.07744

\end{thebibliography}

\end{document}
