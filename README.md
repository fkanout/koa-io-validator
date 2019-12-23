# koa-validator

[![Build Status](https://travis-ci.org/fkanout/koa-validator.svg?branch=master)](https://travis-ci.org/fkanout/koa-validator)
[![codecov](https://codecov.io/gh/fkanout/koa-validator/branch/master/graph/badge.svg)](https://codecov.io/gh/fkanout/koa-validator)
[![Maintainability](https://api.codeclimate.com/v1/badges/8232d29278c06901cd50/maintainability)](https://codeclimate.com/github/fkanout/koa-validator/maintainability)
[![David deps](https://img.shields.io/david/fkanout/koa-validator.svg?style=flat-square)](https://codeclimate.com/github/fkanout/koa-validator)

Koa input/output validation middleware

# Usage

```javascript
import Koa from "koa";
import Router from "@koa/router";

import validate from ('koa-validator');
import Joi from "@hapi/joi"; // Required

const app = new Koa();
const router = new Router()

router.get(
    "/hello/:id",
    validate({
      query: {
        q: Joi.string().required()
      },
      params: {
        id: Joi.string().required()
      },
      headers: {
        "Content-Type": Joi.string()
          .valid("application/json", "application/javascript")
          .required()
      },
      200: {
        succuss: Joi.bool()
      }
    }),
    async (ctx, next) => {
      ctx.body = {
        succuss: true
      };
      await next();
    }
  );

app.use(router.routes());
```
