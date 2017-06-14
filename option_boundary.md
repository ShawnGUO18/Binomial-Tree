# Binomial-Tree
%% calculate the option boundary
function [lattice]=Boundary(S0,K,T,sigma,N)
    deltaT=T/N;
    u=exp(sigma*sqrt(deltaT));
    d=1/u;
    lattice=zeros(N+1,N+1);
    for i=0:N
        lattice(i+1,N+1)=max(0,(S0*(u^(N-i))*(d^i)-K));
    end
