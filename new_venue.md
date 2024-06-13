1. Add to `schema/sql/fx-prod.yaml`
2. Add to `venue_t` in `schema/sql/switchboard.sql`
3. Run `schema/sql/autogen.sh` (it requires `re-gen-sql` in the path, the binary is built by `make build` in `reactive-go` repo and then put into `~/go/bin` by `make install`)
4. Now `switchboard.sql` should have more diffs with `market_group_t` values
5. Run `make` in `schema`
6. Run `docker-compose build` in `schema` (That tries to build sqlite database)
7. `docker-compose down -v`
8. `docker-compose up mariadb` - this creates a local MariaDB database which can be viewed by SQL clients like DBeaver
9. (Optionally) change `prod` to `uat` in `schema/docker-compose.yml` and re-run the last 2 steps. Do not commit this.
