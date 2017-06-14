# Binomial-Tree
%% calculate the up-and-out barrier option
function [lattice,price,stock,boundary]=Option_barrier(r,N)
    deltaT=5/N;
    p=1/2;
    q=1-p;
    [exp_boundary,stock]=Stock(N);
    lattice=exp_boundary;
    for i=0:N
        if stock(i+1,N+1)>125
                lattice(i+1,N+1)=0;
        end
    end
    boundary=lattice;
    for j=N-1:-1:0
        for i=0:j
            if stock(i+1,j+1)>125
                lattice(i+1,j+1)=0;
            else
                lattice(i+1,j+1)=exp(-r*deltaT)*(q*lattice(i+2,j+2)+p*lattice(i+1,j+2));
            end
        end
    end
    price=lattice(1,1);
