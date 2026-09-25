import { serverQueryContent } from "#content/server";
export default async (e) => (await serverQueryContent(e).find()).map((doc) => ({
  link: doc._path,
  title: doc.title
}));
