# before-save-file
Moralis.file
// Changing the file name
Moralis.Cloud.beforeSaveFile(async (request) => {
  const { file } = request;
  const fileData = await file.getData();
  const newFile = new Moralis.File("a-new-file-name.txt", { base64: fileData });
  return newFile;
});

// Returning an already saved file
Moralis.Cloud.beforeSaveFile((request) => {
  const { user } = request;
  const avatar = user.get("avatar"); // this is a Moralis.File that is already saved to the user object
  return avatar;
});

// Saving a different file from uri
Moralis.Cloud.beforeSaveFile((request) => {
  const newFile = new Moralis.File("some-file-name.txt", {
    uri: "www.somewhere.com/file.txt",
  });
  return newFile;
});
