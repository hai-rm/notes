1. Add to `schema/sql/fx-prod.yaml`
2. Add to `venue_t` in `schema/sql/switchboard.sql`
3. Run `schema/sql/autogen.sh`. That requires `re-gen-sql` in the path. The binary is built by `make build` in `reactive-go` repo and then put into `~/go/bin` by `make install`
4. Now `switchboard.sql` should have more diffs with `market_group_t` values
5. Run `make` in `schema`. That tries to add the new sql values to sqlite database
6. Run `sudo docker-compose build` in `schema`
7. `sudo docker-compose down -v`
8. `sudo docker-compose up mariadb`
9. (Optionally) change `prod` to `uat` in `schema/docker-compose.yml` and re-run the last 2 steps. Do not commit this.
