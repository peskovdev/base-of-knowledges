# Basics

### Table of contents
- [Init](#init)
- [Url params](#urlparams)
- [Pydantic validation](#pydantic)



### <a name='init'></a> Init

```py
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}
```

### <a name='urlparams'></a> Url params
```py
# path parameter: /user/13
@app.get("/users/{user_id}")
def func(user_id: int):
    pass

# query parameter: /trades?limit=1&offset=0
@app.get("/trades")
def get_trades(limit: int = 1, offset: int = 0):
    return fake_traders[offset:][:limit]
```

### <a name='pydantic'></a> Pydantic Validation
1) Define models
    ```py
    from pydantic import BaseModel


    class DegreeType(Enum):
        newbie = "newbie"
        expert = "expert"


    class Degree(BaseModel):
        id: int
        created_at: datetime
        type_degree: DegreeType


    class User(BaseModel):
        id: int
        role: str
        name: str
        degree: list[Degree] | None = []


    class Trade(BaseModel):
        id: int
        user_id: int
        currency: str = Field(max_length=5)
        side: str
        price: float = Field(ge=0)
        amount: float
    ```
2) Use for receiving
    ```py
    @app.post("/trades")
    def add_trades(trades: list[Trade]):
        traders.extend(trades)
        return {"status": 200, "data": traders}
    ```
3) Use for sending:
    ```py
    @app.get("/users/{user_id}", response_model=list[User])
    def func(user_id: int):
        return [user for user in users if user.get("id") == user_id]
    ```
    or
    ```py
    @app.get("/users/{user_id}")
    def func(user_id: int) -> list[User]:
        return [user for user in users if user.get("id") == user_id]
    ```
