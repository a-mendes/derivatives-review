# Derivação de Expressões Regulares


Sob o contexto da Teoria da Computação, métodos de derivação são algoritmos  utilizados para definir se determinada cadeia de caracteres pode ser reconhecida por uma Expresão Regular (ER). 

Considerando um símbolo qualquer $\alpha \in \Sigma^*$ e uma linguagem $L$, a derivada de $L$ sobre o símbolo $\alpha$ é denotada por
$$
    \delta_{a}L =  \{w \ |\ \alpha w \in L\}
$$
 
Pela definição de derivação proposta por Brzozowski, primeiramente, considera-se a função auxiliar $v$, definida abaixo, onde $r$ e $s$ representam ERs distintas.

$$
    v(r) =
    \begin{cases}
        \lambda & \text{se } r \text{ é anulável} \\
        \phi & \text{caso contrário}
    \end{cases}
$$

$$
    \begin{align}
        v(\lambda) & = \lambda \\
        v(\alpha) & = \phi \\
        v(r \cdot s) & = v(r) \cap v(s) \\
        v(r \cap s) & = v(r) \cap v(s) \\
        v(r + s) & = v(r) \cup v(s) \\
        v(r^*) & = \lambda \\
        v(¬r) & =
        \begin{cases}
            \phi & \text{se } r \text{ é anulável} \\
            \lambda & \text{caso contrário}
        \end{cases}
    \end{align}
$$

Em sequência, aplicam-se as seguintes regras para derivação

$$
    \begin{align}
        \delta_{\lambda} &= \phi \\
        \delta_{a}a &= \lambda \\
        \delta_{a}b &= \phi, \text{ para } a \neq b \\
        \delta_{a}\phi &= \phi \\
        \delta_{a}(r \cdot s) &= \delta_{a}r \cdot s + v(r) \cdot \delta_{a}s \\
        \delta_{a}(r^*) &= \delta_{a}r \cdot r^* \\
        \delta_{a}(r+s) &= \delta_{a}r + \delta_{a}s \\
        \delta_{a}(r \cap s) &= \delta_{a}r \cap \delta_{a}s \\
        \delta_{a}(¬r) &= ¬(\delta_{a}r) 
    \end{align}
$$

##  Verificação de Pertencimento a uma Expressão Regular

Suponha que desejamos determinar se a palavra $aabb$ pertence à ER $aa + b^*$. Aplicando a derivação de Brzozowski sobre cada caractere da palavra, podemos gerar derivadas da ER até que toda a palavra $aabb$ seja consumida.

$$
\begin{align}
    aa + b^* \sim aabb &\Longleftrightarrow \delta_{a} aa + \delta_{a}b^* &\sim& abb \\
                        &\Longleftrightarrow \delta_{a} a + \delta_{a}b^* &\sim& bb \\
                        &\Longleftrightarrow \delta_{b} b \cdot b^* &\sim& b \\
                        &\Longleftrightarrow \delta_{b} b \cdot b^* &\sim& \lambda \\
 \end{align}
$$

Na equação $(17)$ o primeiro caractere da palavra $aabb$ é consumido aplicando a regra de derivação $(14)$ na ER $aa + b^*$ sobre o simbolo $a$. Em seguida, na equação $(18)$, é aplicada a mesma regra sobre o próximo caractere da palavra.

Nas equações $(19)$ e $(20)$, por sua vez, usa-se a propriedade descrita em $(13)$ para consumir $bb$. O algoritmo, portanto é finalizado com saída $\lambda$ e conclui-se que a palavra $aabb$ pertence à ER $aa + b^*$.